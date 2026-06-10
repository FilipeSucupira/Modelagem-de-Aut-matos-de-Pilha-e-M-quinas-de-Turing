# Descrição Formal: Máquina de Turing - Calculadora de Dano Pokémon Simplificada

**Modelo:** Máquina de Turing Padrão (1 Fita)

A decisão arquitetural de utilizar uma fita única transforma a complexidade combinatória do dano em operações atômicas de adição (+1) e subtração (-1).

## 1. Definição Formal

A Máquina de Turing $M$ é definida pela 7-upla $M = (Q, \Sigma, \Gamma, \delta, q_0, B, F)$, onde:

- $Q = \{q_0, q_{atk\_F}, q_{atk\_W}, q_{atk\_G}, q_{adiciona\_1}, q_{subtrai\_1}, q_{volta\_1}, q_{neutro}, q_{aceita}, q_{rejeita}\}$
- $\Sigma = \{F, W, G, 1\}$
- $\Gamma = \{F, W, G, 1, B\}$ (onde $B$ representa o símbolo Blank)
- $q_0$ é o estado inicial (leitura do tipo do ataque)
- $B$ é o símbolo vazio (Blank)
- $F = \{q_{aceita}\}$ é o conjunto de estados finais

## 2. Função de Transição ($\delta$)

As transições são projetadas na forma de um funil de decisão:
1. **Fase de Classificação (Leitura de Tipos):** O estado inicial lê o ataque e desvia para o estado de memória correspondente ($q_{atk\_F}$, etc). O estado de memória lê a defesa e encaminha a fita para uma das três ações globais.
2. **Fase de Operação (Buff/Debuff):**
   - **$q_{adiciona\_1}$:** Varre todos os `1`s para a direita. Ao encontrar $B$, escreve `1` e aceita.
   - **$q_{subtrai\_1}$:** Varre todos os `1`s para a direita. Ao encontrar $B$, move à esquerda para o estado $q_{volta\_1}$, que apaga o último `1` (substituindo por $B$) e aceita.
   - **$q_{neutro}$:** Varre os `1`s e aceita sem modificar.

## 3. Justificativa de Uso

O uso da MT padrão com uma única fita permite ilustrar perfeitamente as propriedades de varredura (scanning) e modificação in-place da Fita, que são características intrínsecas da Máquina de Turing original proposta por Alan Turing. Esta modelagem é significativamente mais limpa e apresenta um gráfico simétrico ideal para defesa oral.
