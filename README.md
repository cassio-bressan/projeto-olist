# # 🐶 Análise de Raças de Cães com SQL

Este projeto consiste na modelagem, organização e análise de uma base de dados contendo informações sobre raças de cães. Ele abrange a criação de tabelas normalizadas, preenchimento com dados brutos e extração de insights por meio de queries SQL. Foi desenvolvido com fins de aprendizado e portfólio.

## 📁 Estrutura do Projeto

- `Criação de Tabelas/` – Scripts SQL para criar tabelas principais e intermediárias
- `Preenchimento de Tabelas/` – Scripts Python e SQL para inserir os dados no banco
- `Insights/` – Análises e descobertas baseadas nas queries SQL
- `Arquivos/` – Resultados das consultas em formato .csv, notebook de apoio e scripts para conexão com o banco de dados e exportação dos dados
	-	Schema_CTest.ipynb – Verificação da estrutura das tabelas no MySQL
	-	to_csv.ipynb – Script para exportar os resultados das queries como .csv
	-	Resultados_DataFrames.ipynb – Visualização dos resultados das queries diretamente como DataFrames

## 🧠 Técnicas Utilizadas

- Modelagem relacional e normalização de dados
- Criação e uso de chaves primárias e estrangeiras
- Consultas SQL com JOIN, GROUP BY, CTE, HAVING, ORDER BY, LIMIT, entre outras
- Automatização da inserção de dados com Python e PyMySQL
- Identificação e correção de duplicatas


## 💾 Fonte dos Dados

Os dados utilizados neste projeto foram extraídos da seguinte base no Kaggle:

🔗 [Dog Breed Characteristics - Kaggle](https://www.kaggle.com/datasets/marshuu/dog-breeds)


## 🧩 Modelagem do Banco de Dados

O banco foi modelado com base na tabela bruta do Kaggle, utilizando boas práticas de normalização. A modelagem foi feita visualmente no DrawSQL.

🔗 [Visualizar Modelo Relacional no DrawSQL](https://drawsql.app/teams/alone-team-2/diagrams/projeto-racas-caes)



## 📊 Exemplos de perguntas respondidas

- Qual é a doença mais comum entre os cães?
- Quais traços de personalidade são mais comuns em raças pequenas?
- Quais raças compartilham os mesmos problemas de saúde e traços de personalidade?

## 🚀 Como executar

1. Crie um banco de dados no MySQL
2. Rode os scripts SQL de criação de tabelas
3. Execute os notebooks e scripts para preencher as tabelas
4. Explore os insights no arquivo `Insights.md`
5. Para visualizar os insights com melhor formatação no VS Code:
    - Clique com o botão direito no arquivo `Insights.md`
    - Selecione **"Open Preview"** (ou "Abrir visualização")
 > 🔒 Por motivos de segurança, a senha de conexão ao banco de dados foi removida dos arquivos de script.

## 🤖 Apoio com IA

Este projeto foi idealizado, construído e codificado por mim, com apoio pontual da Inteligência Artificial (ChatGPT) para revisão de queries SQL, boas práticas de modelagem relacional, sugestões técnicas e organização final do projeto.