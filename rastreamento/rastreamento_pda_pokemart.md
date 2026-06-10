# Rastreamento de Execução - Autômato de Pilha (Poké Mart)

## Notação
- **Z:** Fundo da Pilha
- **$:** Representa 1 moeda no saldo

## 1. Rastreamento: Compra de Poção (Exata)
**Entrada:** `M M P E`

| Passo | Estado | Símbolo Lido | Pilha Atual | Ação Realizada |
|-------|--------|--------------|-------------|----------------|
| 1 | `q0` | `ε` | `Z` | Inicializa Pilha. Vai p/ `q_idle`. |
| 2 | `q_idle` | `M` | `Z` | Lê 1ª Moeda. Empilha `$`. (Pilha: `$ Z`) |
| 3 | `q_idle` | `M` | `$ Z` | Lê 2ª Moeda. Empilha `$`. (Pilha: `$ $ Z`) |
| 4 | `q_idle` | `P` | `$ $ Z` | Lê Poção. Desempilha 1º `$`. Vai p/ `q_P1`. (Pilha: `$ Z`) |
| 5 | `q_P1` | `ε` | `$ Z` | Transição fantasma. Desempilha 2º `$`. Volta p/ `q_idle`. (Pilha: `Z`) |
| 6 | `q_idle` | `E` | `Z` | Lê Encerrar. Pilha é Z. Vai direto para `q_aceita`. |
| 7 | `q_aceita` | `ε` | `Z` | Finalizado. ACEITA. |

## 2. Rastreamento: Compra com Troco
**Entrada:** `M M M M B E` (4 Moedas, Compra Pokébola [3])

| Passo | Estado | Lendo | Pilha Atual | Ação Realizada |
|-------|--------|-------|-------------|----------------|
| 1-4 | `q_idle`| `M` x4| `Z` -> `$$$$Z`| Inseriu 4 moedas. |
| 5 | `q_idle` | `B` | `$$$$Z` | Lê B. Pop `$`. Vai p/ `q_B1`. (Restam 3 `$`) |
| 6 | `q_B1` | `ε` | `$$$Z` | Transição 2/3. Pop `$`. Vai p/ `q_B2`. (Restam 2 `$`) |
| 7 | `q_B2` | `ε` | `$$Z` | Transição 3/3. Pop `$`. Volta p/ `q_idle`. (Resta 1 `$`) |
| 8 | `q_idle` | `E` | `$Z` | Lê E. Como topo é `$`, vai para `q_troco` e Pop `$`. (Resta `Z`) |
| 9 | `q_troco`| `ε` | `Z` | Topo é Z. Vai para `q_aceita`. |
| 10 | `q_aceita`| `ε`| `Z` | ACEITA. |

## 3. Rastreamento: Rejeição por Saldo Insuficiente
**Entrada:** `M P E` (1 Moeda, Poção [2])

| Passo | Estado | Lendo | Pilha Atual | Ação Realizada |
|-------|--------|-------|-------------|----------------|
| 1-2 | `q_idle`| `M` | `$Z` | Inseriu 1 moeda. |
| 3 | `q_idle` | `P` | `$Z` | Lê P. Pop `$`. Vai p/ `q_P1`. Pilha agora é apenas `Z`. |
| 4 | `q_P1` | `ε` | `Z` | Erro Crítico. O estado exige fazer Pop de `$`, mas o topo é `Z`. O autômato trava. **REJEITA**. |
