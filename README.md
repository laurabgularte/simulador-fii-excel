
# 📊 Simulador de Investimentos em Fundos Imobiliários (FIIs)

Ferramenta interativa desenvolvida em Microsoft Excel para simulação de acúmulo patrimonial e projeção de renda passiva mensal (dividendos) através de Fundos Imobiliários (FIIs), com alocação customizada por perfil de investidor.

> Projeto desenvolvido como Desafio de Projeto da formação na **DIO (Digital Innovation One)** sob orientação do Expert **Felipe Aguiar (Felipão)**.

---

## ❓ Perguntas que a Ferramenta Responde

A ferramenta foi estruturada para responder diretamente às 5 perguntas fundamentais de negócio do investidor:

| Pergunta de Negócio                          | Onde aparece a resposta na planilha                                                  |
| :------------------------------------------- | :----------------------------------------------------------------------------------- |
| **1. Quanto investir por mês?**              | Painel de Entrada (`C6`) — com campo editável de aporte e sugestão de 30% do salário |
| **2. Por quantos anos?**                     | Painel de Entrada (`C7`) — definição do prazo total do projeto                       |
| **3. Qual a taxa de rendimento mensal?**     | Painel de Entrada (`C8`) — taxa percentual de dividend yield médio projetado         |
| **4. Quanto de patrimônio vai acumular?**    | Card de Resultado Principal e Tabela de Projeção (2 a 30 anos)                       |
| **5. Quanto vai receber de dividendos/mês?** | Card de Resultado Principal e Tabela de Projeção (calculado sobre o saldo final)     |

---

## 🧮 Lógica de Cálculos e Fórmulas

### 1. Função `VF` (Valor Futuro)

A função `VF` é utilizada para calcular o patrimônio acumulado ao longo do tempo considerando os aportes mensais e a taxa de juros composta.

```excel
=VF(taxa_mensal; prazo_anos * 12; -aporte; 0)
```

- **`taxa_mensal`:** Rendimento mensal aplicado.
- **`prazo_anos * 12`:** Conversão do prazo em anos para total de meses.
- **`-aporte`:** O valor mensal investido (com sinal negativo, pois representa saída de caixa para o Excel).
- **`0`:** Indica que não há patrimônio inicial prévio (ou valor presente zerado).

### 2. Função `PROCV` com Chave Composta

Para determinar o percentual de investimento em cada um dos 6 tipos de FIIs, foi utilizada uma **chave composta**, pois o `PROCV` tradicional realiza buscas baseadas em apenas uma coluna.

```excel
=PROCV(perfil_investidor & Tipo_FII; Apoio!$A$2:$D$19; 4; FALSO)
```

- **Concatenação (`&`):** Junta o perfil escolhido (`Conservador`, `Moderado` ou `Arrojado`) com o nome do tipo de fundo (ex: `Tijolo - Shopping`).
- **Busca:** Procura o texto resultante (ex: `"ConservadorTijolo - Shopping"`) na matriz da aba `Apoio`.
- **Retorno:** Retorna a 4ª coluna da tabela de apoio, correspondente ao percentual exato daquela combinação.

---

## 🏷️ Intervalos Nomeados Criados

Para evitar o uso de referências obscuras como `C4` ou `C8` e tornar as fórmulas legíveis para qualquer usuário, foram cadastrados os seguintes intervalos nomeados:

- **`salario`**: Célula do salário mensal informado pelo usuário.
- **`sugestao_aporte`**: Célula com o cálculo de 30% do salário (`=salario * 0,30`).
- **`aporte`**: Célula com o valor mensal efetivamente aplicado no simulador.
- **`prazo_anos`**: Célula com a quantidade de anos da simulação.
- **`taxa_mensal`**: Célula com a taxa de dividend yield estimada ao mês.
- **`perfil_investidor`**: Célula com a seleção do perfil via validação de dados em lista.

---

## 📊 Percentuais de Cada Perfil e Origem

A divisão da carteira entre os 6 tipos de fundos imobiliários segue uma lógica de diversificação e tolerância a risco. **Cada perfil soma exatamente 100%**:

| Tipo de FII                 | Conservador | Moderado | Arrojado | Origem / Racional Estratégico                     |
| :-------------------------- | :---------: | :------: | :------: | :------------------------------------------------ |
| **Tijolo - Shopping**       |     10%     |   20%    |   25%    | Foco em valorização e resiliência no varejo       |
| **Tijolo - Logística**      |     25%     |   25%    |   20%    | Contratos atípicos e previsibilidade de caixa     |
| **Tijolo - Escritórios**    |     15%     |   15%    |   20%    | Renda imobiliária corporativa de grande porte     |
| **Papel / CRIs**            |     35%     |   20%    |   10%    | Alta proteção contra inflação e previsibilidade   |
| **FoFs (Fundos de Fundos)** |     10%     |   10%    |   10%    | Diversificação automática via gestão profissional |
| **Híbridos / Outros**       |     5%      |   10%    |   15%    | Busca por maior alpha/retorno suplementar         |
| **TOTAL**                   |  **100%**   | **100%** | **100%** | **Garantia de alocação integral dos aportes**     |

_Origem das estimativas:_ Alocações baseadas em relatórios públicos de análise de mercado e recomendações genéricas de diversificação patrimonial (utilizadas apenas para fins didáticos).

---

## 🔄 Mudanças em Relação à Ferramenta do Expert

Para agregar valor e evoluir o projeto original do Felipão, foram implementadas as seguintes melhorias:

1. **Gráfico Dinâmico de Rosca:** Adicionada visualização gráfica da distribuição da carteira que se atualiza automaticamente ao alterar o perfil no menu suspenso.
2. **Cenário Alternativo com Sugestão de 30%:** Implementado um comparativo visual mostrando a diferença patrimonial final entre investir o aporte informado versus a sugestão automatizada de 30% do salário.
3. **Formatação de Aplicativo:** Ocultação de barras de fórmulas, títulos de linhas/colunas e linhas de grade para oferecer uma experiência limpa de uso.

## ✅ Checklist de Validação Antes do Envio

- [x] A planilha abre sem erro de fórmula e responde às cinco perguntas.
- [x] Trocar o perfil na lista muda a divisão do aporte, e cada perfil soma 100%.
- [x] O salário e os valores do arquivo publicado são fictícios/exemplo.

