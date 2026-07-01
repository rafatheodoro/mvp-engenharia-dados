# Pipeline de Engenharia de Dados em Databricks para Análise de Cargos e Remuneração dos Servidores Públicos Federais

![Databricks](https://img.shields.io/badge/Databricks-EF3E42?logo=databricks&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-FDEE21?logo=apachespark&logoColor=black)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD8?logo=databricks&logoColor=white)
![Data Engineering](https://img.shields.io/badge/Data%20Engineering-0052CC?logo=apache&logoColor=white)
![PUC--Rio](https://img.shields.io/badge/PUC--Rio-003366?logo=academia&logoColor=white)

## Resumo do Projeto

| Item | Descrição |
|---|---|
| **Tema** | Cargos e remuneração dos servidores públicos federais |
| **Período analisado** | Outubro de 2025 |
| **Fonte** | Portal da Transparência do Governo Federal |
| **Plataforma** | Databricks Free Edition |
| **Arquitetura** | Staging → Bronze → Silver → Gold |
| **Modelo analítico** | Esquema estrela com tabelas fato e dimensões |
| **Foco técnico** | Engenharia de Dados, Data Quality, Delta Lake e Modelagem Dimensional |

---

## Resumo Executivo

Este projeto foi desenvolvido como trabalho final da disciplina de **Engenharia de Dados** da Pós-Graduação em **Data Science & Analytics (PUC-Rio)**, aplicando conceitos de Data Lakehouse, arquitetura em camadas e modelagem dimensional sobre dados públicos do Governo Federal.

A solução utiliza **Databricks**, **Apache Spark/PySpark**, **Spark SQL** e **Delta Lake** para construir um pipeline capaz de ingerir, tratar, padronizar e modelar dados cadastrais e remuneratórios de servidores públicos federais civis do Poder Executivo.

O resultado é uma camada analítica estruturada em modelo estrela, permitindo consultas sobre distribuição de servidores, órgãos, cargos, vínculos funcionais, remuneração média, indenizações e limitações de completude dos dados.

---

## Arquitetura da Solução

```text
                         ┌──────────────────────────────┐
                         │ Portal da Transparência GovBR │
                         │ Servidores e Aposentados      │
                         │ Outubro/2025                  │
                         └───────────────┬──────────────┘
                                         │
                                         ▼
                         ┌──────────────────────────────┐
                         │ Databricks                   │
                         │ Catálogo: servidores         │
                         │ Schemas: staging/bronze/     │
                         │ silver/gold                  │
                         └───────────────┬──────────────┘
                                         │
                                         ▼
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐
│ Staging      │ → │ Bronze       │ → │ Silver       │ → │ Gold             │
│ Arquivos ZIP │   │ Dados brutos │   │ Dados limpos │   │ Modelo estrela   │
│ e CSVs       │   │ Delta Tables │   │ e tratados   │   │ Fatos e dimensões│
└──────────────┘   └──────────────┘   └──────────────┘   └────────┬─────────┘
                                                                  │
                                                                  ▼
                                            ┌──────────────────────────────┐
                                            │ Consultas Analíticas         │
                                            │ Indicadores Gerenciais       │
                                            │ Cargos | Órgãos | Vínculos   │
                                            │ Remuneração | Indenizações   │
                                            └──────────────────────────────┘
```

---

## Problema

Os dados públicos de servidores federais são disponibilizados em arquivos extensos, com estruturas distintas, campos sensíveis, inconsistências de nomenclatura, formatos financeiros textuais, datas em diferentes padrões e lacunas em alguns atributos relevantes.

Para que esses dados possam ser usados em análises gerenciais, é necessário construir um pipeline capaz de organizar, tratar, documentar e modelar as informações em uma estrutura analítica confiável.

---

## Objetivo

Construir um pipeline de Engenharia de Dados em Databricks para transformar dados brutos do Portal da Transparência em uma base analítica estruturada, permitindo análises sobre cargos, órgãos, vínculos funcionais e remuneração dos servidores públicos federais civis do Poder Executivo.

---

## Questões Analíticas

O projeto buscou responder questões como:

- Qual o quantitativo total de servidores analisados?
- Quais órgãos concentram o maior número de servidores?
- Quais cargos possuem maior representatividade?
- Quais órgãos e cargos apresentam maior remuneração média?
- Como os servidores estão distribuídos por UF de exercício?
- Qual o total de indenizações por órgão e cargo?
- Quais limitações da base impedem determinadas análises gerenciais?

---

## Fonte dos Dados

Os dados foram obtidos no **Portal da Transparência do Governo Federal**, referentes a **Outubro de 2025**.

Arquivos utilizados:

- `202510_Servidores_SIAPE`
- `202510_Aposentados_SIAPE`

O escopo considera servidores públicos federais civis do Poder Executivo, excluindo carreiras militares e servidores do Banco Central (BACEN).

---

## Tecnologias Utilizadas

- Databricks Free Edition
- Apache Spark
- PySpark
- Spark SQL
- Delta Lake
- DBFS / Volumes Databricks
- Python
- SQL
- Modelo Dimensional / Star Schema

---

## Competências Técnicas Aplicadas

- Engenharia de Dados
- Arquitetura Medallion
- Data Lakehouse
- Ingestão e persistência com Delta Lake
- Limpeza e padronização de dados
- Data Quality
- Modelagem Dimensional
- Construção de tabelas fato e dimensões
- Criação de catálogo, schemas e volumes
- Consultas analíticas com Spark SQL

---

## Principais Entregas

- Criação do catálogo `servidores` e dos schemas `staging`, `bronze`, `silver` e `gold`;
- Ingestão dos arquivos públicos do Portal da Transparência;
- Persistência dos dados brutos em Delta Tables na camada Bronze;
- Tratamento, padronização e validação dos dados na camada Silver;
- Remoção de colunas sensíveis e campos sem valor analítico;
- Conversão de campos financeiros e datas para tipos adequados;
- Criação de chaves e dimensões auxiliares;
- Implementação de modelo dimensional na camada Gold;
- Execução de consultas analíticas sobre servidores, cargos, órgãos e remuneração.

---

## Principais Análises

As consultas desenvolvidas permitiram identificar:

- **630.557** servidores distintos na base analisada;
- Ministério da Saúde como órgão com maior concentração de servidores;
- Professor do Magistério Superior como cargo com maior quantidade de servidores;
- Advocacia-Geral da União como órgão com maior remuneração média;
- distribuição de servidores por UF de exercício;
- remuneração média por UF;
- cargos com maiores médias remuneratórias;
- total de indenizações por órgão e cargo;
- remuneração média por tipo de vínculo.

Também foram identificadas limitações importantes para análises de afastamento, vacância, sexo, idade e tempo de serviço, devido à ausência ou baixa completude desses atributos na fonte original.

---

## Qualidade dos Dados

Durante o pipeline foram aplicadas ações de qualidade e governança, incluindo:

- padronização de nomes de colunas;
- tratamento de valores nulos e inválidos;
- remoção de dados sensíveis, como CPF e matrícula;
- conversão de campos financeiros para valores numéricos;
- conversão e padronização de datas;
- validação de unicidade e integridade referencial;
- criação de chaves artificiais para cargos e vínculos;
- documentação de tabelas e colunas no catálogo.

Essas etapas foram essenciais para tornar os dados adequados ao consumo analítico.

---

## Limitações

A análise está limitada aos dados disponíveis para **Outubro de 2025**, sem contemplar séries históricas. Algumas perguntas não puderam ser respondidas porque a base não possui informações suficientes sobre vacância, sexo/gênero, idade, tempo de serviço e classificação detalhada de licenças ou afastamentos.

---

## Possíveis Evoluções

- Construção de dashboards interativos;
- Inclusão de séries históricas para análise temporal;
- Integração com dados de outros poderes e fontes complementares;
- Automatização do catálogo e da documentação dos dados;
- Ampliação das métricas gerenciais e indicadores derivados;
- Evolução para análises preditivas e comparativos históricos.
