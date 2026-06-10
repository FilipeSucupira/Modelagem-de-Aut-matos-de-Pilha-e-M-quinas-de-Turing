# Rastreamento de Execução - MT Calculadora de Dano (1 Fita)

## 1. Rastreamento: Super Efetivo (+1 Dano)
**Entrada:** `F G 1 1 1`

| Passo | Estado | Fita (Cabeçote entre colchetes) | Ação Executada |
|-------|--------|---------------------------------|----------------|
| 0 | `q0` | `[F] G 1 1 1 B` | Lê `F`, escreve `F`, move `R` |
| 1 | `q_atk_F` | `F [G] 1 1 1 B` | Lê `G`, escreve `G`, move `R` |
| 2 | `q_adiciona_1` | `F G [1] 1 1 B` | Lê `1`, escreve `1`, move `R` |
| 3 | `q_adiciona_1` | `F G 1 [1] 1 B` | Lê `1`, escreve `1`, move `R` |
| 4 | `q_adiciona_1` | `F G 1 1 [1] B` | Lê `1`, escreve `1`, move `R` |
| 5 | `q_adiciona_1` | `F G 1 1 1 [B]` | Lê `B`, escreve `1`, move `S` |
| 6 | `q_aceita` | `F G 1 1 1 [1]` | Máquina para e Aceita |

## 2. Rastreamento: Pouco Efetivo (-1 Dano)
**Entrada:** `W G 1 1 1`

| Passo | Estado | Fita (Cabeçote entre colchetes) | Ação Executada |
|-------|--------|---------------------------------|----------------|
| 0 | `q0` | `[W] G 1 1 1 B` | Lê `W`, escreve `W`, move `R` |
| 1 | `q_atk_W` | `W [G] 1 1 1 B` | Lê `G`, escreve `G`, move `R` |
| 2 | `q_subtrai_1` | `W G [1] 1 1 B` | Lê `1`, escreve `1`, move `R` |
| 3 | `q_subtrai_1` | `W G 1 [1] 1 B` | Lê `1`, escreve `1`, move `R` |
| 4 | `q_subtrai_1` | `W G 1 1 [1] B` | Lê `1`, escreve `1`, move `R` |
| 5 | `q_subtrai_1` | `W G 1 1 1 [B]` | Lê `B`, escreve `B`, move `L` |
| 6 | `q_volta_1` | `W G 1 1 [1] B` | Lê `1`, escreve `B`, move `S` |
| 7 | `q_aceita` | `W G 1 1 [B] B` | Máquina para e Aceita |
