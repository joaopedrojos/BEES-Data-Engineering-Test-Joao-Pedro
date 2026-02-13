# BEES-Data-Engineering-Test-Joao-Pedro

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/3910d7e5-2315-4253-8d4f-101934fa77ec" />

# Arquitetura de Dados no Databricks (Medallion Architecture)

Esta solução foi construída sobre a plataforma **Databricks**, utilizando o padrão **Medallion Architecture (Bronze, Silver, Gold)** com armazenamento em **Delta Lake** e processamento via **Apache Spark**, governado pelo **Unity Catalog**.

O objetivo desta arquitetura é garantir **governança**, **qualidade**, **rastreabilidade** e **confiabilidade** dos dados desde a ingestão até o consumo analítico e de Machine Learning.

---

## 🔹 Fontes de Dados

A arquitetura suporta ingestão de dados em dois formatos:

- **Batch Data**: cargas periódicas provenientes de arquivos, bancos relacionais ou APIs.
- **Streaming Data**: ingestão contínua de eventos em tempo real.

Esses dados são direcionados para a camada inicial do Data Lake sem transformações, preservando o dado bruto para auditoria e reprocessamento.

---

## 🔹 Orquestração

A orquestração dos pipelines é realizada por meio de **Jobs e Pipelines do Databricks**, responsáveis por:

- Executar cargas batch e streaming
- Aplicar regras de transformação entre as camadas
- Garantir reprocessamento controlado
- Manter a ordem e dependência entre etapas do pipeline

---

## 🔹 Governança com Unity Catalog

Todo o ambiente é governado pelo **Unity Catalog**, que provê:

- Controle de acesso baseado em papéis (RBAC)
- Catálogo centralizado de tabelas e schemas
- Auditoria e rastreabilidade de uso dos dados
- Padronização dos objetos de dados

---

## 🔹 Camadas do Data Lake (Medallion)

### 🥉 Bronze — Raw Data
- Armazena os dados exatamente como foram recebidos da fonte
- Sem regras de negócio
- Mantém histórico completo para auditoria
- Base para reprocessamentos

### 🥈 Silver — Clean & Validated Data
- Aplicação de regras de qualidade e validações
- Tratamento de nulos, tipos, duplicidades e inconsistências
- Padronização de estruturas
- Dados prontos para uso analítico confiável

### 🥇 Gold — Business Ready Data
- Dados agregados e modelados para consumo
- Aplicação de regras de negócio
- Tabelas otimizadas para BI, dashboards e modelos de ML
- Camada de alto desempenho para leitura

---

## 🔹 Processamento de Dados

O processamento é realizado utilizando **Apache Spark** sobre tabelas **Delta Lake**, permitindo:

- Transações ACID
- Versionamento de dados (Time Travel)
- Alta performance em leitura e escrita
- Suporte nativo a batch e streaming no mesmo pipeline

---

## 🔹 Observabilidade

A arquitetura conta com monitoramento ativo por meio de **Alertas do Databricks**, permitindo:

- Monitorar regras de qualidade de dados
- Detectar anomalias nos pipelines
- Notificar falhas ou desvios automaticamente
- Garantir confiabilidade operacional

---

## 🔹 Consumo dos Dados

A camada Gold é consumida por:

- Ferramentas de **BI e Dashboards**
- Modelos de **Machine Learning**
- Usuários analíticos e times de negócio

Essa separação garante que os consumidores utilizem apenas dados confiáveis, validados e governados.

