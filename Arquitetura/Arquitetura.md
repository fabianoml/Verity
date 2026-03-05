# Verity — Visão Geral da Arquitetura

## 1. Visão Geral do Sistema

A plataforma **Verity** foi projetada para automatizar a concessão de crédito para **Pequenas e Médias Empresas (PMEs)** utilizando uma arquitetura híbrida que combina **Machine Learning tradicional** e **Inteligência Artificial Generativa**.

O sistema processa aproximadamente:

- **10.000 solicitações de crédito por dia**
- Dados financeiros estruturados
- Documentos não estruturados como e-mails, contratos e notícias de mercado

O objetivo da solução é fornecer **decisões automáticas de crédito com justificativas explicáveis**, minimizando riscos financeiros e operacionais.

---

# 2. Princípios Arquiteturais

A arquitetura foi projetada com base nos seguintes princípios:

- Arquitetura híbrida de IA
- Eficiência de custos (FinOps)
- Explicabilidade e auditabilidade
- Segurança desde a concepção (*Security by Design*)
- Infraestrutura escalável nativa em nuvem

A solução utiliza serviços da **Google Cloud Platform (GCP)**.

Principais serviços utilizados:

- BigQuery
- Vertex AI
- Cloud DLP
- Document AI
- Cloud Run
- Vertex AI Vector Search

---

# 3. Arquitetura de Alto Nível

A solução é dividida em quatro camadas principais.

---

## Camada de Dados

Responsável pelo armazenamento e gerenciamento dos dados estruturados financeiros.

Componentes principais:

- **BigQuery**
- **Feature Store**

Os dados armazenados incluem:

- histórico transacional
- balanços financeiros
- dados cadastrais de clientes

Esses dados são utilizados para alimentar os modelos de risco.

---

## Camada de Processamento de Documentos

Responsável pela ingestão e processamento de dados não estruturados.

Principais componentes:

- **Document AI** para extração de texto via OCR
- **Cloud Data Loss Prevention (DLP)** para detecção de dados sensíveis
- **Vertex AI** para geração de embeddings

Os documentos processados são armazenados em um banco vetorial para permitir **busca semântica**.

---

## Motor de Decisão de Risco

O cálculo do score de risco é realizado utilizando **modelos tradicionais de Machine Learning**.

Modelo principal utilizado:

- **XGBoost**

O modelo calcula o score de risco com base em features estruturadas recuperadas da **Feature Store**.

Vantagens dessa abordagem:

- resultados determinísticos
- alto desempenho em dados tabulares
- menor custo computacional
- maior interpretabilidade

---

## Motor de Contexto e Justificativa

Modelos de **IA generativa** são utilizados para interpretar informações contextuais e produzir justificativas explicáveis para as decisões de crédito.

A solução utiliza uma arquitetura baseada em **RAG (Retrieval-Augmented Generation)**.

Fluxo de funcionamento:

1. Recuperação de features estruturadas da **Feature Store**
2. Recuperação de documentos relevantes via **banco vetorial**
3. Construção de um prompt com evidências
4. Geração da justificativa usando **Gemini**

Essa abordagem garante que as justificativas sejam **baseadas em evidências reais e auditáveis**.

---

# 4. Orquestração Agent-to-Agent (A2A)

A plataforma utiliza uma arquitetura baseada em **agentes especializados**.

### Agente de Risco

Responsável pela análise quantitativa.

Funções:

- recuperação de features
- cálculo do score de crédito
- avaliação de thresholds de risco

---

### Agente de Contexto

Responsável pela análise textual e contextual.

Funções:

- recuperação semântica de documentos
- análise de contexto
- geração de justificativa

---

Ambos os agentes colaboram para produzir a **decisão final de crédito**.

---

# 5. Segurança e Privacidade

O sistema processa informações financeiras e dados pessoais sensíveis.

Medidas de segurança implementadas:

- detecção de PII utilizando **Cloud DLP**
- mascaramento e tokenização de dados sensíveis
- controle de acesso via **IAM**
- isolamento de serviços via **VPC Service Controls**

Esses mecanismos garantem conformidade com **LGPD e regulamentações financeiras**.

---

# 6. Estratégia FinOps

Para controlar os custos operacionais de IA, o sistema utiliza uma estratégia de **inferência em camadas**.

Distribuição estimada das requisições:

- **70%** resolvidas pelo modelo XGBoost
- **20%** analisadas pelo modelo **Gemini Flash**
- **10%** enviadas para **Gemini Pro**

Essa abordagem reduz significativamente os custos associados ao uso de modelos generativos.

---

# 7. Governança e Observabilidade

Para garantir rastreabilidade e auditabilidade:

- todas as decisões são registradas
- prompts e respostas do modelo são armazenados
- features utilizadas na decisão são registradas

Os logs são centralizados no **BigQuery** para auditoria e monitoramento.

---

# 8. Escalabilidade

A plataforma foi projetada para escalar horizontalmente utilizando serviços gerenciados da GCP:

- inferência serverless
- banco vetorial escalável
- processamento distribuído de dados

Essa arquitetura permite suportar crescimento no volume de solicitações sem grandes alterações estruturais.

---

# 9. Conclusão

A arquitetura da plataforma **Verity** equilibra desempenho, explicabilidade, eficiência de custos e segurança.

Ao combinar **Machine Learning tradicional com IA generativa**, a solução permite:

- automação escalável de decisões de crédito
- geração de justificativas baseadas em evidências
- governança robusta de dados
- controle eficiente de custos operacionais
