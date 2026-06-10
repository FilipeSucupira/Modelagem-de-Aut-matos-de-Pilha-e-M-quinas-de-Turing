# Casos de Teste - MT Calculadora de Dano (Simplificada de 1 Fita)

## Bateria de Testes

1. **Ataque Super Efetivo (+1 de Dano):**
   - **Entrada:** `F G 1 1 1` (Ataque Fogo, Defensor Grama, Dano Base 3)
   - **Resultado Esperado:** ACEITA. Fita final: `F G 1 1 1 1` (Dano Final 4)

2. **Ataque Pouco Efetivo (-1 de Dano):**
   - **Entrada:** `W G 1 1 1` (Ataque Água, Defensor Grama, Dano Base 3)
   - **Resultado Esperado:** ACEITA. Fita final: `W G 1 1 B` (Dano Final 2)

3. **Ataque Neutro (Dano Mantido):**
   - **Entrada:** `G G 1 1` (Ataque Grama, Defensor Grama, Dano Base 2)
   - **Resultado Esperado:** ACEITA. Fita final: `G G 1 1` (Dano Final 2)

4. **Entrada Inválida (Rejeição):**
   - **Entrada:** `1 F 1` (Começa com número ao invés de Tipo de Ataque)
   - **Resultado Esperado:** REJEITA. Máquina entra no estado `q_rejeita`.
