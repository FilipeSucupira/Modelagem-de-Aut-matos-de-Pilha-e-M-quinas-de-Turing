# Roteiro de Apresentação - AV2 Teoria da Computabilidade

Este documento serve como um guia/roteiro para vocês montarem os slides (`.pptx` ou Canva) e saberem exatamente o que falar na hora da defesa oral.

---

## Slide 1: Capa
- **Título Sugerido:** Teoria da Computabilidade no Universo Pokémon
- **Subtítulo:** Modelagem de Autômatos de Pilha e Máquinas de Turing
- **Texto:** Disciplina: Teoria da Computabilidade | Professor: Daniel Leal Souza
- **Imagem:** Uma capa legal dividida no meio. De um lado um desenho de uma Poké Mart (Lojinha), do outro uma arena de Batalha Pokémon clássica de GameBoy.
- **Dica de Fala:** "Bom dia/boa noite professor e turma. Nós somos a equipe composta por [Nomes] e hoje vamos apresentar o nosso projeto prático, onde utilizamos Autômatos e Máquinas de Turing para recriar mecânicas clássicas dos jogos de Pokémon."

---

## Slide 2: As Máquinas Escolhidas
- **Título:** Modelos Computacionais Selecionados
- **Texto em Tópicos:** 
  - Problema 1: Loja Pokémon (Poké Mart)
  - Modelo 1: Autômato de Pilha (PDA)
  - Problema 2: Calculadora de Dano em Batalhas
  - Modelo 2: Máquina de Turing Padrão (1 Fita)
- **Imagem:** Ícone de uma pilha (stack) de moedas de um lado, e um desenho de uma fita perfurada (Turing) do outro.
- **Dica de Fala:** "Para atender à regra da AV2, escolhemos exatamente dois modelos distintos: O Autômato de Pilha para gerenciar o dinheiro infinito em compras, e a Máquina de Turing clássica de 1 Fita para calcular as operações in-place da matemática do dano."

---

## Slide 3: Problema 1 - Poké Mart
- **Título:** Sistema de Compras Poké Mart
- **Texto:** 
  - **Desafio:** Como processar inserção infinita de moedas, realizar descontos dinâmicos e devolver troco matematicamente exato?
  - A linguagem de moedas não é uma Linguagem Regular (não resolve com Autômato Finito).
- **Imagem:** Screenshot de uma Pokébola, Poção e Antídoto com os preços ao lado.
- **Dica de Fala:** "No jogo, você joga dinheiro na loja e compra itens. A quantidade de dinheiro que você insere não tem limite. Um Autômato Finito falharia aqui pois não tem memória infinita para contar moedas. Por isso, precisávamos de um Autômato de Pilha."

---

## Slide 4: Autômato de Pilha em Ação
- **Título:** Modelagem do Autômato de Pilha (PDA)
- **Texto:** 
  - `$`: Fundo de Pilha
  - **Ação de Push:** Empilha `X` para cada Moeda (`M`) lida.
  - **Ação de Pop:** Desempilha `X` para pagar os itens.
  - **Estado de Troco:** Esvazia o restante devolvendo moedas reais até chegar no `$`.
- **Imagem:** Print screen do JFLAP do arquivo `pda_pokemart.jff` focado nos loops (a estrela do projeto).
- **Dica de Fala:** "Nós projetamos o PDA para usar a pilha literalmente como uma carteira física. Cada 'M' joga um 'X' na pilha. Quando compramos uma poção, que custa 2, o estado dá um 'Pop' consecutivo em 2 'X's."

---

## Slide 5: Problema 2 - Batalha e Vantagem de Tipo
- **Título:** O Algoritmo de Dano Pokémon
- **Texto:**
  - **Desafio:** Ler o Tipo do Ataque, ler o Tipo da Defesa, identificar se é Vantajoso ou Desvantajoso e alterar o Dano Base proporcionalmente.
  - Fogo ganha de Grama, Água ganha de Fogo, Grama ganha de Água.
- **Imagem:** Um gráfico clássico ou triângulo das fraquezas (Fogo > Grama > Água > Fogo).
- **Dica de Fala:** "No nosso segundo modelo, fomos para a batalha. Se uso Fogo contra Grama, o jogo me dá bônus de dano. Se eu uso Água contra Grama, eu sofro penalidade. Como matematizar isso e fazer o próprio autômato processar o bônus?"

---

## Slide 6: A Solução Elegante com Máquina de Turing
- **Título:** Máquina de Turing Padrão (1 Fita)
- **Texto:**
  - **Varredura (Scanning):** A máquina lê os tipos no começo da fita e guarda na "memória" (Estado Interno).
  - **Operação In-Place:** Ela navega pelos marcadores de dano (`111`) até achar o espaço em branco (`B`).
  - **Modificador:** Se Super Efetivo, ela escreve um `1` extra (+1). Se Pouco Efetivo, ela apaga o último `1` (-1).
- **Imagem:** Print screen limpo do funil do JFLAP `mt_dano.jff` (destaque para a simetria da máquina).
- **Dica de Fala:** *(IMPORTANTE PARA DEFESA)* "Professor, optamos por usar a **Máquina de Turing Padrão (de 1 fita)** de propósito. Ela ilustra lindamente o conceito de 'Varredura de Turing'. A máquina guarda o tipo do golpe no seu estado interno e navega até o fim da fita para processar um +1 ou -1 dinâmico diretamente na memória in-place."

---

## Slide 7: Rastreamento (Execution Trace)
- **Título:** Rastreamento Passo a Passo
- **Texto:**
  - **Entrada:** `F G 1 1 1` (Ataque Fogo, Defensor Grama, Dano Base 3).
  - *Transição q0:* Identifica `F`.
  - *Transição q_atk_F:* Lê `G` (Identifica Super Efetivo).
  - *Loop Adição:* Percorre os `1`s e transforma o primeiro `Blank` em `1`.
  - **Saída Final:** `F G 1 1 1 1` (Dano Final 4) -> **Aceita**.
- **Imagem:** Uma simulação ou gif/print da aba de Step by State do JFLAP mostrando o bloco vermelho indo até o final da fita e escrevendo o `1`.
- **Dica de Fala:** "Aqui podemos ver a mágica acontecendo na prática. Fogo vs Grama é Super Efetivo. A cabeça de leitura engole os `1`s e anexa o bônus no final."

---

## Slide 8: Conclusão
- **Título:** Conclusão e Declaração de Uso de IA
- **Texto:** 
  - A conversão de lógicas de videogames em modelagens computacionais abstratas demonstra o rigor matemático por trás do entretenimento.
  - Utilizamos a IA (Google Gemini) como suporte técnico para formatação de arquivos JFLAP e redação da documentação matemática em Markdown (vide declaração oficial entregue).
- **Imagem:** Uma imagem legal misturando um professor universitário e um mestre Pokémon.
- **Dica de Fala:** "Para finalizar, esse trabalho nos provou que todo jogo que amamos jogar no celular ou no console, lá no fundo, se resume à teoria dos autômatos clássicos esvaziando pilhas de moedas ou varrendo fitas para somar +1 de dano de fogo."
