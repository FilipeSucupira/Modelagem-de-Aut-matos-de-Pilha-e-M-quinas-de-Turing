# Descrição Formal: Autômato de Pilha - Poké Mart

**Modelo:** Autômato de Pilha (PDA)

## 1. Definição Formal

O Autômato de Pilha $P$ é definido por $P = (Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$, onde:

- $Q = \{q_0, q_{idle}, q_{P1}, q_{B1}, q_{B2}, q_{R1}, q_{R2}, q_{R3}, q_{R4}, q_{troco}, q_{aceita}\}$
- $\Sigma = \{M, P, B, R, E\}$ (Alfabeto de entrada)
  - M = Inserir Moeda (1 de saldo)
  - P = Comprar Poção (Custo 2)
  - B = Comprar Pokébola (Custo 3)
  - R = Comprar Revive (Custo 5)
  - E = Encerrar/Troco
- $\Gamma = \{Z, \$\}$ (Alfabeto da pilha)
- $q_0$: Estado inicial
- $Z_0 = Z$: Símbolo inicial da pilha (fundo)
- $F = \{q_{aceita}\}$: Estado de aceitação final

## 2. Lógica de Transição ($\delta$)

A máquina utiliza a Pilha como um acumulador numérico unário (carteira de moedas).

**Fase 1: Inserção de Moedas ($q_{idle}$)**
- $\delta(q_{idle}, M, Z) = (q_{idle}, \$Z)$
- $\delta(q_{idle}, M, \$) = (q_{idle}, \$\$)$
Ao ler 'M', um símbolo `$` é empilhado, contabilizando o saldo.

**Fase 2: Compras e Dedução do Saldo**
Para deduzir um valor $N > 1$, o PDA lê a entrada, desempilha um `$`, e transita por $N-1$ estados em épsilon ($\varepsilon$) para desempilhar o restante, voltando ao estado idle.
- **Poção (Custo 2):** $q_{idle}$ lê `P`, faz pop `$`, vai para $q_{P1}$. Em $q_{P1}$, lê $\varepsilon$, faz pop `$`, volta para $q_{idle}$.
- **Pokébola (Custo 3):** $q_{idle}$ lê `B`, faz pop `$`, vai para $q_{B1} \rightarrow q_{B2} \rightarrow q_{idle}$, com pops adicionais em cada etapa.
- **Revive (Custo 5):** $q_{idle}$ lê `R`, e cascateia por 4 estados intermédios ($q_{R1} \dots q_{R4}$) fazendo pop em cada um.
*(Se não houver saldo suficiente na pilha para concluir o pop, o autômato trava e rejeita a palavra, agindo como bloqueio de saldo insuficiente).*

**Fase 3: Encerrar e Troco**
- O usuário envia `E`. O PDA vai para $q_{troco}$, fazendo um loop de $\varepsilon$ para desempilhar todos os `$` restantes (liberando o troco fictício).
- Quando encontra o fundo $Z$, ele lê $\varepsilon$, faz pop $Z$, e transita para o $q_{aceita}$.

## 3. Justificativa de Complexidade

Um PDA permite aceitar linguagens não regulares que dependem de contagem. O número de estados ($11$) é alcançado de forma **totalmente orgânica e imperativa**. Em autômatos de pilha clássicos, ler uma letra da fita restringe a operação da pilha a no máximo um "pop". Portanto, modelar a "subtração de $N$ unidades de saldo" exige passar por $N-1$ estados auxiliares com transições vazias. Isso prova que os estados não foram inflados artificialmente, mas sim gerados pela matemática natural do preço dos itens.
