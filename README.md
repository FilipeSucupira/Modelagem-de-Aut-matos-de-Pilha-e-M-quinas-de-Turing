# AV2 – Teoria da Computabilidade
## Máquinas Universais, Turing e Autômatos de Pilha

**Disciplina:** Teoria da Computabilidade  
**Professor:** Daniel Leal Souza  
**Semestre:** 01/2026  
**Turma:** CC5MA / CC5NA  

---

## 👥 Integrantes

| Nome | Matrícula |
|------|-----------|
| Andrey Lourival Andrade Garcia
| Everton Gustavo de Oliveira
| Filipe César Sucupira Maciel
| Igor Cecim Vilhena

---

## 🤖 Máquinas/Modelos Escolhidos

| # | Modelo | Problema Resolvido (Temática Pokémon) |
|---|--------|----------------------------------------|
| 1 | **Máquina de Turing Padrão (1 Fita)** | **Calculadora de Dano Pokémon:** Lê os tipos de ataque e defesa e aplica uma modificação in-place na fita adicionando (+1) ou subtraindo (-1) dano baseado em vantagens. |
| 2 | **Autômato de Pilha – PDA** | **Poké Mart (Vending Machine):** Controle de saldo ilimitado em pilha, múltiplas compras e devolução de troco através de `pop` de saldo. |

---

## 📁 Estrutura do Repositório

```text
projeto_av2/
├── README.md                          ← Este arquivo
├── uso_ia.md                          ← Declaração de uso de IA
├── referencias.md                     ← Referências bibliográficas
├── relatorio_rastreamento.md          ← Relatório curto de rastreamento de execução (Exigência da Lauda)
├── roteiro_apresentacao.md            ← Roteiro para a apresentação do slide
│
├── slides/
│   └── (coloque_seu_slide_aqui).pdf   ← Slides da apresentação
│
├── implementacoes/
│   ├── mt_dano_pokemon/
│   │   ├── mt_dano.jff                ← Arquivo JFLAP da MT
│   │   └── descricao_formal.md        ← Formalização matemática e justificativa de estados
│   │
│   └── pda_pokemart/
│       ├── pda_pokemart.jff           ← Arquivo JFLAP do PDA
│       └── descricao_formal.md        ← Formalização matemática e justificativa de estados
│
├── testes/
│   ├── testes_mt_dano.md              ← Bateria de testes MT
│   └── testes_pda_pokemart.md         ← Bateria de testes PDA
│
└── rastreamento/
    ├── rastreamento_mt_dano.md        ← Trace detalhado MT
    └── rastreamento_pda_pokemart.md   ← Trace detalhado PDA
```

---

## ▶️ Como Executar

### Pré-requisitos
- **JFLAP 7.1** (download em: https://www.jflap.org/jflap/)
- Java 8 ou superior instalado

### Passos para abrir e executar

1. Abra o JFLAP (`java -jar JFLAP.jar`)
2. Vá em `File > Open`
3. Navegue até a pasta `implementacoes/` correspondente
4. Abra o arquivo `.jff` desejado
5. Para testar uma entrada:
   - Clique em `Input > Multiple Run` (para testar vários casos)
   - Ou `Input > Step by State` (para ver a fita/pilha em tempo real)

### Exemplos de Entrada Rápida

**MT Padrão (Calculadora de Dano):**
- Entrada única: `FG111` (Sem espaços: Ataque Fogo, Defesa Grama, Dano 3)
- *Resultado Esperado:* A máquina varrerá a fita e adicionará um `1` no final, gerando `FG1111` (Super Efetivo, Dano 4).

**PDA Poké Mart:**
- Entrada: `M M M M B E` (Insere 4 Moedas, Compra Pokébola[3], Pede Troco)
- *Resultado Esperado:* Aceita. A pilha será esvaziada corretamente devolvendo o troco, e a máquina encerra em estado de aceitação.

---

## 📚 Referências

Veja o arquivo [referencias.md](referencias.md).
