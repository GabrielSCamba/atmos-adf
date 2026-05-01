# atmos-adf

Projeto de Engenharia de Dados utilizando Azure Data Factory (ADF) para ingestão, orquestração e armazenamento de dados meteorológicos em ambiente cloud.

O projeto realiza integrações com diferentes fontes de dados, incluindo APIs e BigQuery, armazenando os dados em Azure Data Lake Storage Gen2 para posterior processamento analítico.

---

# Arquitetura da Solução

O projeto foi desenvolvido utilizando serviços do ecossistema Azure com foco em ingestão e orquestração de pipelines de dados.

```text
Fontes de Dados
    │
    ├── Visual Crossing API
    ├── BigQuery (INMET)
    │
    ▼
Azure Data Factory
    │
    ▼
Azure Data Lake Storage Gen2
    │
    ▼
Camada Landing / Raw
    │
    ▼
Processamento no Databricks
```

---

# Objetivos do Projeto

* Automatizar ingestão de dados meteorológicos
* Centralizar dados em Data Lake
* Implementar pipelines parametrizados
* Demonstrar integração entre serviços cloud
* Aplicar boas práticas de Engenharia de Dados
* Construir base para arquitetura Lakehouse

---

# Estrutura do Projeto

```text
atmos-adf/
│
├── dataset/
├── linkedService/
├── pipeline/
├── trigger/
└── README.md
```

---

# Componentes do Projeto

## Pipelines

### pl_ingest_inmet_landing_dev

Pipeline responsável pela ingestão de dados do INMET.

Principais responsabilidades:

* Leitura de dados meteorológicos
* Integração com fonte externa
* Escrita no ADLS Gen2
* Organização em camada landing

---

### pl_ingest_visualcrossing_landing_dev_daily

Pipeline responsável pela ingestão diária de dados da API Visual Crossing.

Características:

* Execução recorrente
* Ingestão automatizada
* Armazenamento incremental
* Estruturação dos dados no Data Lake

---

### pl_ingest_visualcrossing_landing_dev_daily_history

Pipeline voltado para ingestão histórica da API Visual Crossing.

Principais funcionalidades:

* Coleta de dados históricos
* Processamento por período
* Parametrização de datas
* Armazenamento em formato estruturado

---

# Linked Services

## ls_adlsg2_atmos_dev

Conexão com Azure Data Lake Storage Gen2.

Responsável por:

* Armazenamento dos arquivos
* Persistência dos dados brutos
* Integração com pipelines do ADF

---

## ls_akv_atmos_dev

Integração com Azure Key Vault.

Responsável por:

* Gerenciamento seguro de secrets
* Armazenamento de credenciais
* Integração segura com APIs e serviços

---

## ls_bigquery_inmet_dev

Conexão com Google BigQuery.

Responsável por:

* Leitura de dados do INMET
* Integração multi-cloud
* Extração de dados meteorológicos

---

## ls_http_visualcrossing_dev

Conexão HTTP com a API Visual Crossing.

Responsável por:

* Consumo da API meteorológica
* Requisições HTTP automatizadas
* Coleta de dados climáticos

---

# Datasets

## ds_bigquery_inmet_src_dev

Dataset de origem para dados do BigQuery.

---

## ds_csv_inmet_landing_dev

Dataset responsável pelo armazenamento de arquivos CSV no Data Lake.

---

## ds_js_visualcrossing_landing_dev

Dataset utilizado para persistência de arquivos JSON da Visual Crossing.

---

## ds_json_visualcrossing_src_dev

Dataset de origem da API Visual Crossing.

---

# Triggers

## tr_daily_visualcrossing_dev

Trigger responsável pela execução automática diária dos pipelines de ingestão.

Objetivos:

* Automatizar execução
* Garantir atualização recorrente
* Reduzir processos manuais

---

# Tecnologias Utilizadas

* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Key Vault
* Google BigQuery
* REST API
* JSON
* CSV
* Databricks

---

# Conceitos Aplicados

* ETL/ELT
* Data Lake
* Orquestração de pipelines
* Integração multi-cloud
* Parametrização
* Ingestão incremental
* Governança de credenciais
* Automação de processos
* Arquitetura moderna de dados

---

# Segurança

O projeto utiliza Azure Key Vault para armazenamento seguro de credenciais e secrets utilizados pelos pipelines.

Benefícios:

* Evita exposição de chaves
* Centraliza gerenciamento de secrets
* Melhora governança e segurança

---

# Fluxo de Ingestão

## Visual Crossing

```text
Visual Crossing API
        │
        ▼
Azure Data Factory
        │
        ▼
ADLS Gen2 (Landing)
```
