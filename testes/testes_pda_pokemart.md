# Casos de Teste - PDA Máquina de Vendas Poké Mart

## Bateria de Testes

1. **Compra Exata:**
   - **Entrada:** `M M P E` (2 Moedas, 1 Poção, Encerrar)
   - **Resultado Esperado:** ACEITA. (Saldo zera exatamente com a compra, encerra na hora).

2. **Compra com Troco:**
   - **Entrada:** `M M M M B E` (4 Moedas, 1 Pokébola [custa 3], Encerrar)
   - **Resultado Esperado:** ACEITA. O troco de 1 moeda (`$`) será jogado fora pela fase de encerramento.

3. **Compra Múltipla:**
   - **Entrada:** `M M M M M M M P R E` (7 Moedas. 1 Poção [2], 1 Revive [5])
   - **Resultado Esperado:** ACEITA. Custo total exato de 7.

4. **Rejeição por Falta de Saldo:**
   - **Entrada:** `M M B E` (2 Moedas, Pokébola custa 3).
   - **Resultado Esperado:** REJEITA. O Autômato travará durante os estados intermédios de cobrança da Pokébola (tentará fazer pop de `$`, mas encontrará o fundo `Z`), falhando silenciosamente sem chegar ao estado de aceitação.

5. **Apenas Inserção (Desistência):**
   - **Entrada:** `M M M E` (3 moedas, desiste)
   - **Resultado Esperado:** ACEITA. O estado de troco irá desempilhar as 3 moedas e finalizar.
