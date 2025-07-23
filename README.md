# Analise-de-vendas
Dashboard de análise de vendas e lucratividade para varejo de produtos de consumo, com foco em otimização de custos e volume.

Análise de Vendas e Lucratividade para Varejo Local

William Ames

Visão Geral do Projeto

Este projeto consiste em uma análise aprofundada de dados de vendas e lucratividade de uma empresa varejista que comercializa produtos de consumo. O objetivo principal foi identificar padrões de desempenho de produtos, otimizar estratégias de precificação e custos, e fornecer insights acionáveis para melhorar a rentabilidade do negócio. A análise focou em métricas-chave como lucro, custo de produtos vendidos (CPV), unidades vendidas e taxas de desconto. Para fazer a análise de dados foi utilizado o Power BI, o que permitiu a criação de um dashboard interativo e dinâmico.

Problema de Negócio Abordado

A análise busca responder à seguinte pergunta central:
Quais produtos estão impulsionando (ou prejudicando) nosso lucro, e quais oportunidades temos para otimizar nossas estratégias de vendas? Que produtos podem ser problemáticos?

Para isso, exploramos as seguintes dores de negócio comuns em pequenos e médios varejistas:
Onde estão nossos produtos mais lucrativos? (Será que os produtos que mais vendem são os mesmo que geram mais lucros?);
Por que as vendas estão ou não crescendo como esperado em certos produtos? (Análise de tendências e desempenho);
Como otimizar a aplicação de descontos para maximizar vendas sem corroer o lucro? (Os descontos são a causa das vendas?);

Fonte de Dados

O dataset utilizado para esta análise foi obtido via Kaggle (financial.csv). Ele contém informações detalhadas sobre transações de venda, incluindo:

Produto: Item vendido;

Faixa de Desconto: Categoria de desconto aplicada (ex: Alto, Médio, Nenhum);

Unidades Vendidas: Quantidade de itens vendidos em uma transação;

Preço de Fabricação: Custo unitário de produção;

Preço de Venda: Preço unitário pelo qual o produto foi vendido;

Vendas Brutas: Vendas antes da aplicação de descontos;

Descontos: Valor total dos descontos aplicados;

Vendas (Líquidas): Vendas após a aplicação de descontos (Vendas Brutas - Descontos);

CPV (Custo dos Produtos Vendidos): Custo total dos bens vendidos;

Lucro: Lucro gerado por transação (Vendas Líquidas - CPV);

Data: Data da transação;


Ferramentas Utilizadas

Power BI Desktop: Para limpeza, transformação, modelagem e visualização dos dados.

Power Query Editor: Etapas de ETL (Extração, Transformação e Carga).

DAX: Para criação de medidas e cálculos complexos (se houver, como porcentagem de lucro, etc.).

Processo de Limpeza e Transformação de Dados (ETL com Power Query)

1.  Remoção de Colunas Irrelevantes: 
As colunas País e Segmento foram removidas, pois o foco da análise é em varejo local, tornando esses dados desnecessários e potencialmente distrativos. Colunas de data redundantes (Mês Número, Mês Nome, Ano) também foram removidas, utilizando apenas a coluna Data principal.

2.   Tratamento de Valores Nulos e Inconsistências:
 Valores “$-” na coluna Descontos foram substituídos por “0”, assumindo que “$-” indica ausência de desconto;

 Linhas com “-” (sinal de menos) em colunas numéricas foram limpas, substituindo o “-” por “0” antes da conversão de tipo;

4.  Conversão de Tipos de Dados com Localidade:
Todas as colunas contendo valores monetários (Preço de Fabricação, Preço de Venda, Vendas Brutas, Descontos, Vendas, CPV, Lucro) foram convertidas para o tipo Número Decimal utilizando a localidade Inglês (Estados Unidos). Isso garantiu a correta interpretação do separador decimal (.) e de milhares (,) no formato original dos dados, preservando a precisão dos centavos (e.g., 32,370.00 foi corretamente convertido para 32370.00).

5.  Inconsistência Observada:
Durante a validação de dados, foi notada uma inconsistência entre `Preço de Fabricação` e CPV (onde Unidades Vendidas * Preço de Fabricação não correspondia ao CPV fornecido). . Para os fins desta análise, optou-se por confiar nos valores de CPV e Lucro conforme fornecidos no dataset, uma vez que o CPV é o custo total e o Lucro é derivado diretamente das vendas e do CPV. A coluna Preço de Fabricação foi mantida para fins de possíveis visualizações futuras.

6.  Renomeação de Colunas: 
As colunas foram renomeadas para o português para facilitar a compreensão e a criação dos relatórios  (Sales para Vendas, Profit para Lucro, etc.) 

Principais Insights e Análises 
Cartões de KPI: 

Total de Vendas: R$127,93 Milhões;

Lucro Total: R$ 16,89 Milhões;

Unidades vendidas: 1,13 Milhões;

Gráficos:

Lucro por Unidades Vendidas e Desempenho de Volume:
Este gráfico de colunas e linhas analisa o Lucro Total em relação ao Volume de Unidades Vendidas por produto. Foi observado que o produto Paseo é o que mais vende e, consequentemente, o que mais gera lucro em termos absolutos. Este visual ajuda a identificar produtos que, além de rentáveis, contribuem significativamente para o volume geral de vendas, indicando forte demanda

Análise de Margem: Lucro vs. Custo dos Produtos Vendidos (CPV):
Este gráfico de colunas e linhas compara o Lucro Total (barras) e o Custo dos Produtos Vendidos (CPV - linha) por produto. Foi avaliado que, embora o Paseo seja o produto com maior lucro absoluto, ele também apresenta os maiores custos, resultando em uma margem apertada. Por outro lado, os produtos Amarilla e Carretera demonstram um lucro muito bom com custos significativamente inferiores, resultando em excelentes margens de lucratividade. Estes são, portanto, os itens mais eficientes.
Nota sobre a Escala Visual: 
É importante observar que, neste gráfico, embora o Custo dos Produtos Vendidos (CPV) total seja numericamente um valor significativamente maior que o Lucro total (dada a natureza do cálculo de margem, onde Lucro = Vendas - CPV), a representação visual da linha do CPV pode parecer mais baixa que as barras de Lucro. Isso ocorre devido à otimização automática das escalas dos dois eixos Y independentes do gráfico. Para uma leitura precisa dos valores, consulte os rótulos de dados diretamente nas barras e na linha.
Impacto da Estratégia de Descontos na Lucratividade:
Para entender a influência dos descontos, uma medida DAX (Taxa Média de Desconto %) foi criada, calculando a porcentagem média do desconto em relação ao lucro. Ao analisar o Lucro Total por produto em conjunto com essa taxa, observou-se que a variação das taxas de desconto é relativamente baixa, oscilando entre 6,63% e 7,95% para a maioria dos produtos. 

Conclusão: Essa baixa variação percentual indica que os produtos, incluindo o Paseo, não dependem de grandes promoções ou descontos agressivos para venderem bem. Isso reforça a análise de que a margem apertada do Paseo está mais relacionada a um alto custo intrínseco (CPV) do que a uma política de descontos insustentável
Recomendações 

Projeção de Lucro por Aumento de Volume:

 Tendo em vista o potencial de crescimento em lucro dos produtos com alta margem em comparação com custos, por exemplo Amarilla e Carretera, foi implementada uma análise "e se" que simula o impacto de um aumento no volume de produção (e vendas).
Para que isso fosse possível, uma medida DAX dinâmica (`Lucro Projetado Cenário`) e uma segmentação de dados interativa foram criadas e implementadas, permitindo ao usuário do dashboard ajustar um multiplicador de volume (ex: 1x, 2x, 3x a produção atual)
Sendo possível, portanto, a demonstração visual do aumento exponencial do lucro total que pode ser alcançado ao focar no crescimento da venda de produtos com margens saudáveis. Por exemplo, ao dobrar o volume de produção de Amarilla e Carretera, observa-se um crescimento significativo no lucro projetado.
Recomendação: Investir em estratégias para aumentar o volume de vendas de produtos como Amarilla e Carretera, que já possuem alta margem de lucro e não dependem de grandes descontos. A ferramenta de projeção ilustra claramente o retorno potencial dessas estratégias.

Oportunidade de Otimização de Custos:

Identificou-se uma grande oportunidade para otimização de custos, especialmente para produtos como o Paseo, que, apesar de gerarem alto volume de lucro total, possuem margens apertadas devido a custos de produção elevados, e não por excesso de descontos.
Para investigar o potencial impacto da redução de custos no lucro, foi implementada uma análise "e se" no Power BI. Para tanto, uma medida DAX dinâmica (`Lucro Projetado com Redução de Custo`) e uma segmentação de dados interativa foram criadas e implementadas, permitindo, assim, simular diferentes percentuais de redução no **Custo dos Produtos Vendidos (CPV)
Ao fazer essa análise foi possível observar que uma pequena e totalmente possível redução de 10% nos custos totais (CPV) poderia gerar um aumento de quase R$ 11 milhões no lucro geral Esta é uma descoberta de alto impacto, que justifica um foco estratégico na renegociação com fornecedores bem como otimizar os processos de custo para os produtos com CPV elevado, como o Paseo.
Recomendação: Priorizar uma auditoria e negociação de custos para produtos com CPV desproporcionalmente alto. O cenário "e se" demonstra o retorno financeiro direto dessa iniciativa.
