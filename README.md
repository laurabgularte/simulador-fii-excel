# 💰 Simulador de Investimentos em Fundos Imobiliários (FIIs)

Ferramenta desenvolvida em Excel com foco em experiência de usuário (estilo aplicativo) para simulação de investimentos em Fundos Imobiliários, automatizando o cálculo de aportes, projeção de patrimônio a longo prazo e distribuição inteligente de ativos conforme o perfil de risco do investidor.

---

## 🎯 Perguntas de Negócio que a Ferramenta Responde

A planilha foi projetada para responder de forma rápida e intuitiva a cinco perguntas essenciais para qualquer investidor:
1. **Quanto investir por mês?** $\rightarrow$ Definido na seção de investimentos mensais (com sugestão automatizada baseada em 30% do salário).
2. **Por quantos anos?** $\rightarrow$ Definido pelo horizonte de tempo da simulação.
3. **Qual a taxa de rendimento mensal?** $\rightarrow$ Taxa esperada de retorno sobre o capital aplicado.
4. **Quanto de patrimônio vai acumular?** $\rightarrow$ Calculado dinamicamente utilizando a função `VF` (*Future Value*).
5. **Quanto vai receber de dividendos por mês?** $\rightarrow$ Renda passiva mensal gerada a partir do patrimônio acumulado e do rendimento da carteira.

As respostas principais ficam evidentes no painel principal da **Planilha1 (Calculadora)**.

---

## ⚙️ Como os Cálculos e Funções Entram na Ferramenta

* **Função VF (Future Value):** Utilizada para projetar o crescimento do patrimônio composto ao longo dos meses. 
  * *Fórmula aplicada:* `=VF(TAXA_MENSAL, QTD_ANOS*12, APORTE*-1)`
* **PROCV com Chave Composta:** Na aba de apoio (`Planilha2`), foi criada uma coluna de chave composta (`PERFIL-TIPO DE FII`) unindo o perfil do investidor ao tipo de fundo. Na calculadora, o `VLOOKUP` busca automaticamente o percentual correspondente ao perfil selecionado na lista suspensa.
  * *Fórmula aplicada:* `=VLOOKUP($C$23&"-"&B27, Planilha2!$A:$D, 4, FALSE)`

---

## 🏷️ Intervalos Nomeados Criados

Para facilitar a leitura das fórmulas e manutenção da planilha, foram definidos os seguintes intervalos nomeados:
* `SALARIO`: Célula de referência para remuneração mensal.
* `SUG_INVESTIMENTO`: Sugestão de aporte de 30% do salário.
* `APORTE`: Valor efetivamente investido por mês.
* `QTD_ANOS`: Horizonte de tempo da simulação.
* `TAXA_MENSAL`: Taxa de rendimento aplicada por mês.
* `PATRIMONIO`: Resultado do patrimônio acumulado.
* `REND_CARTEIRA`: Taxa de retorno de dividendos da carteira.

---

## 📊 Perfis de Investidor e Distribuição de Aportes

A tabela de apoio (`Planilha2`) estrutura a alocação percentual para cada perfil, garantindo que a soma de cada categoria seja exatamente **100%**:

* **Conservador:** 30% Papel | 50% Tijolo | 10% Híbridos | 10% FOFs | 0% Desenvolvimento | 0% Hotelarias *(Total: 100%)*
* **Moderado:** 32% Papel | 35% Tijolo | 8% Híbridos | 5% FOFs | 10% Desenvolvimento | 10% Hotelarias *(Total: 100%)*
* **Agressivo:** 50% Papel | 10% Tijolo | 5% Híbridos | 5% FOFs | 20% Desenvolvimento | 10% Hotelarias *(Total: 100%)*

---

## 🚀 O que foi Evoluído na Ferramenta

* **Interface Limpa:** Linhas de grade ocultas e formatação condicional/visual com cara de dashboard corporativo.
* **Automação de Aporte:** Sugestão inteligente de 30% do salário integrada por fórmula nomeada.
* **Dinâmica por Perfil:** Validação de dados em lista suspensa na célula de perfil, alterando instantaneamente a divisão do aporte entre os 6 tipos de FIIs na tabela inferior.

---

