# Relatório Curto de Rastreamento de Execução

Este relatório documenta a execução bem-sucedida das duas máquinas implementadas para a AV2, validando sua aceitação de acordo com a teoria da computabilidade.

## 1. Máquina de Turing Padrão (Calculadora de Dano Pokémon)
**Objetivo:** Ler os tipos do ataque e defesa, e aplicar uma operação matemática in-place (+1 de dano para super efetivo) ao final da fita.

- **Entrada Testada:** `F G 1 1 1` (Ataque Fogo, Defensor Grama, Dano Base 3)
- **Rastreamento Resumido:**
  1. **[q0]:** Cabeçote lê `F` (Ataque). A máquina entra no estado de memória `q_atk_F`, deslocando-se para a direita.
  2. **[q_atk_F]:** Lê `G` (Defesa). Identifica a relação "Super Efetivo". Transita para o funil `q_adiciona_1` deslocando-se para a direita.
  3. **[q_adiciona_1]:** Máquina varre toda a sequência de `1`s (dano base) realizando movimentos iterativos para a direita (Loop).
  4. **[q_adiciona_1]:** Cabeçote encontra o primeiro símbolo `Blank` ($B$). Substitui $B$ por `1` (aplicando o buff de dano).
  5. **[q_aceita]:** Máquina entra no estado final de aceitação.
- **Saída Final na Fita:** `F G 1 1 1 1` (Dano Total = 4). ACEITA.

## 2. Autômato de Pilha (Poké Mart)
**Objetivo:** Simular um controle de saldo ilimitado baseado no empilhamento de moedas, permitindo compras e esvaziamento correto para devolução de troco.

- **Entrada Testada:** `M M M P E` (Insere 3 moedas, Compra 1 Poção [custa 2 moedas], Encerra/Troco).
- **Rastreamento Resumido:**
  1. **[q0]:** Inicialização. Adiciona símbolo de fundo de pilha `$`. Transita para `q_idle`.
  2. **[q_idle]:** Lê `M`, faz Push de `X` (moeda 1).
  3. **[q_idle]:** Lê `M`, faz Push de `X` (moeda 2).
  4. **[q_idle]:** Lê `M`, faz Push de `X` (moeda 3). *Pilha atual: `[$, X, X, X]`*.
  5. **[q_idle]:** Lê `P` (Poção). Entra no fluxo de pagamento. Consome (Pop) o primeiro `X`. Transita para `q_pag_1`.
  6. **[q_pag_1]:** Transição épsilon consumindo (Pop) o segundo `X`. Retorna para `q_idle`. *Pilha atual: `[$, X]`*.
  7. **[q_idle]:** Lê `E` (Encerrar). Transita para o loop de devolução de troco `q_troco`.
  8. **[q_troco]:** Consome (Pop) o último `X` restante (devolvendo o troco). *Pilha atual: `[$]`*.
  9. **[q_troco]:** Lê o fundo da pilha `$`, faz Pop. Transita para `q_aceita`.
- **Resultado:** Pilha vazia, fita de entrada toda consumida. ACEITA.
