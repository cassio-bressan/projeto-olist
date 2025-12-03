# Análise de Dados – Operação Logística & Satisfação do Cliente

## 1. Contexto do Projeto
A operação logística é um dos principais fatores que influenciam a experiência do cliente no e-commerce. Atrasos na entrega podem impactar diretamente a satisfação, a reputação da empresa e a recorrência de compras.

Este projeto analisa dados reais de pedidos da Olist com o objetivo de **avaliar o desempenho das entregas**, identificar **padrões de atraso** e entender **como esses atrasos afetam a satisfação dos clientes**.

## 2. Visão Geral dos Dados
A análise foi construída a partir de quatro bases principais, já tratadas e consolidadas:

- **atrasos_por_seller.csv**: contém a taxa de atraso e o atraso médio em dias por vendedor, permitindo avaliar o desempenho logístico individual.
- **atrasos_por_estado.csv**: apresenta os indicadores de atraso agregados por estado, permitindo a análise geográfica.
- **atraso_vs_score.csv**: mostra a nota média dos pedidos em dois cenários: entregas no prazo e entregas atrasadas.
- **probabilidade_nota1.csv**: informa a probabilidade de um pedido receber nota 1 quando há atraso e quando não há atraso.

Essas bases foram utilizadas diretamente na construção dos dashboards e na geração dos principais insights do projeto.

## 3. Principais KPIs (Dashboard de KPIs)
O dashboard de KPIs apresenta uma visão geral do desempenho das entregas na operação analisada. Os principais indicadores são:

- **Taxa de pedidos atrasados:** percentual de pedidos entregues fora do prazo.
- **Atraso médio (dias):** média de dias de atraso dos pedidos atrasados.
- **Tempo médio de entrega real (dias):** tempo médio entre a compra e a entrega efetiva.
- **Tempo médio estimado (dias):** prazo médio informado ao cliente no momento da compra.
- **Diferença (estimado − real):** diferença média entre o prazo estimado e o prazo real de entrega, indicando o erro da estimativa.


Esses KPIs permitem uma avaliação rápida da eficiência logística e da confiabilidade das estimativas de entrega.

## 4. Análise Logística
A análise por vendedor mostrou que existe um grupo de sellers com **taxas de atraso extremamente elevadas**, concentrando a maior parte dos problemas logísticos. Além disso, alguns vendedores apresentam **atraso médio em dias significativamente superior ao restante da base**, indicando gargalos operacionais específicos.

Os resultados indicam que os atrasos **não estão distribuídos de forma homogênea** entre os sellers, sugerindo oportunidades claras de atuação direcionada nos piores desempenhos.

## 5. Análise Geográfica
Os atrasos apresentam **concentração regional bem definida**. Estados do **Nordeste, como Alagoas (AL), Maranhão (MA), Sergipe (SE) e Piauí (PI)**, lideram o ranking de **maior taxa de pedidos atrasados**, indicando maior recorrência de falhas logísticas nessas regiões.

Por outro lado, o **maior atraso médio em dias** está concentrado principalmente nos **estados da Região Norte**, como **Roraima (RR), Amapá (AP) e Amazonas (AM)**, sugerindo que, além de menos frequentes em alguns casos, os atrasos nessas localidades tendem a ser **mais longos quando ocorrem**.

Esse padrão evidencia dois comportamentos distintos:
- Regiões com **alto volume de atrasos frequentes** (principalmente Nordeste);
- Regiões com **atrasos mais longos**, associados a desafios de distância e infraestrutura (principalmente Norte).

Os resultados indicam a necessidade de **estratégias logísticas regionalizadas**, com foco em eficiência operacional no Nordeste e redução do tempo de ciclo nas regiões mais distantes dos centros de distribuição.

## 6. Análise de Satisfação do Cliente
Os resultados evidenciam um **impacto direto e expressivo dos atrasos na percepção do cliente**. Pedidos entregues dentro do prazo apresentam **score médio de 4,1**, enquanto pedidos atrasados registram apenas **2,5**, uma queda de aproximadamente **39% na avaliação**.

Além disso, a **probabilidade de um pedido receber nota mínima (1)** salta de **10% nos pedidos no prazo para 45% nos pedidos atrasados**, indicando um aumento de **4,5 vezes no risco de avaliações extremamente negativas** quando ocorre atraso.

Esses dados confirmam que o atraso na entrega é um dos **principais vetores de insatisfação do cliente**, afetando não apenas a média das avaliações, mas também intensificando fortemente a ocorrência de experiências críticas.

## 7. Impactos no Negócio
Os atrasos logísticos geram impactos diretos em quatro frentes críticas do negócio. No pilar operacional, refletem ineficiências na cadeia de entrega, aumentando custos com retrabalho, suporte e possíveis reentregas. Na experiência do cliente, os dados mostram queda expressiva no score médio e forte aumento no risco de avaliações extremamente negativas.

Do ponto de vista de reputação, a alta concentração de notas baixas associadas a atrasos compromete a imagem da plataforma, afetando a confiança do consumidor e a taxa de recompra. Por fim, há impacto financeiro indireto, uma vez que clientes insatisfeitos tendem a reduzir recorrência, aumentar custos de aquisição e pressionar margens no médio e longo prazo.

## 8. Recomendações
Com base nos resultados apresentados, recomenda-se a priorização de ações focadas em redução de atrasos, controle operacional e mitigação do impacto na experiência do cliente.

No curto prazo, é essencial atuar sobre os estados e sellers com maiores taxas e médias de atraso, estabelecendo planos de correção específicos e acompanhamento contínuo por meio de metas operacionais. Também é recomendado o uso dos KPIs como indicadores de performance ativa, com monitoramento periódico.

No médio prazo, ajustes nos prazos estimados de entrega devem ser realizados para refletir melhor a realidade logística, reduzindo frustração do cliente e avaliações negativas. Adicionalmente, estratégias de comunicação proativa com clientes em pedidos com risco de atraso podem mitigar o impacto na satisfação.

Como ação estratégica, a empresa deve utilizar os dados de atraso como critério para avaliação de parceiros logísticos e vendedores, reforçando padrões mínimos de desempenho operacional.

## 9. Conclusão
A análise evidenciou que os atrasos logísticos possuem impacto direto e significativo na satisfação dos clientes, reduzindo o score médio das avaliações e aumentando fortemente a probabilidade de notas mínimas. Além disso, foi possível identificar diferenças relevantes de desempenho entre estados e operações, indicando gargalos logísticos específicos por região.

Os KPIs analisados mostram que parte dos prazos estimados não reflete a realidade operacional, o que contribui para a frustração do cliente e perda de reputação da empresa. Esse cenário reforça a necessidade de ajustes nos prazos, maior controle sobre sellers e aprimoramento da gestão logística.

De forma geral, os dados geram insumos claros para decisões estratégicas voltadas à eficiência operacional, melhoria da experiência do cliente e redução de impactos negativos na imagem e nos resultados do negócio.