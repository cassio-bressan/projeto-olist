# # 🚚 Análise de Atrasos de Entrega e Impacto na Satisfação do Cliente — Olist

Este projeto consiste na extração, tratamento e análise de dados de pedidos de e-commerce da Olist, com foco no estudo de atrasos nas entregas e seu impacto na satisfação do cliente. Ele abrange a construção de uma base analítica a partir de SQL, o tratamento e geração de métricas em Python e a apresentação dos resultados por meio de dashboards no Excel. Foi desenvolvido com fins de aprendizado e portfólio.

## 📁 Estrutura do Projeto

- `Arquivos/` – Contém a base de dados bruta extraída do MySQL e o código responsável pela conexão com o banco de dados e extração da view final utilizada na análise.

- `Tabelas/` – Contém as tabelas analíticas em formato CSV geradas a partir da análise em Python e utilizadas para alimentar os dashboards.

- `Projeto/` – Reúne os principais artefatos do projeto analítico.
	- `Análise.ipynb` – Notebook com o tratamento dos dados, criação das variáveis analíticas, cálculo dos KPIs e geração dos arquivos CSV.
	- `Dashboard.xlsx` – Arquivo com os dashboards interativos de KPIs, logística, análise geográfica e satisfação do cliente.
	- `Insights.MD` – Documento com a interpretação executiva dos resultados e principais conclusões do projeto.

## 🧠 Técnicas Utilizadas

- Extração de dados em SQL a partir de múltiplas tabelas relacionais
- Criação de views analíticas para consolidação das informações
- Tratamento e limpeza de dados com Python (pandas)
- Criação de variáveis analíticas e KPIs operacionais
- Análise exploratória de dados (EDA)
- Geração de bases analíticas em formato CSV
- Construção de dashboards interativos no Excel
- Análise do impacto logístico na satisfação do cliente

## 💻 Tecnologias utilizadas  
- Python 3.11.7  
- Jupyter Notebook  
- Microsoft Excel  
- MySQL  

## 💾 Fonte dos Dados

Os dados utilizados neste projeto foram extraídos da seguinte base no Kaggle:

🔗 [Brazilian E-Commerce Public Dataset by Olist - Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/versions/7)


## 📊 Exemplos de perguntas respondidas

- Qual é a taxa de pedidos entregues com atraso?
- Qual é o atraso médio em dias nas entregas?
- Qual é a diferença entre o tempo estimado e o tempo real de entrega?
- Como o atraso impacta a avaliação (score) dos clientes?
- Quais estados apresentam os maiores índices de atraso?

## 👀 Como visualizar os resultados

1. Abra o arquivo `Dashboard.xlsx` para visualizar os resultados e indicadores
2. Para visualizar os insights com melhor formatação no VS Code:
    - Clique com o botão direito no arquivo `Insights.md`
    - Selecione **"Open Preview"** (ou "Abrir visualização")

## 🎨 Legenda de Cores dos Dashboards

- 🟢 Verde: desempenho positivo / dentro do esperado
- 🔴 Vermelho: desempenho crítico / atraso ou impacto negativo
- 🟡 Amarelo: alerta / métrica que exige atenção
- 🔵 Azul: indicador neutro / informativo

## 🤖 Apoio com IA

Este projeto foi idealizado, construído e codificado por mim, com apoio pontual da Inteligência Artificial (Gemini) para revisão de queries SQL e códigos Python, boas práticas de modelagem relacional, sugestões técnicas e organização final do projeto.
 > 🔒 Por motivos de segurança, a senha de conexão ao banco de dados foi removida dos arquivos de script.