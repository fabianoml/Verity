# 🧠 Desafio Verity  
## Analista de Crédito Híbrido (Hybrid Credit Analyst)

Este desafio propõe o desenho de uma **arquitetura de dados e IA na Google Cloud Platform (GCP)** para automatizar a concessão de crédito para **PMEs**, combinando **Machine Learning clássico** e **GenAI**.

---

# 🎯 Contexto do Cenário

Uma instituição financeira digital **GCP First** está automatizando seu processo de concessão de crédito.

O sistema deve analisar tanto **dados estruturados quanto não estruturados** para tomar decisões automáticas.

### 📊 Dados Estruturados
Armazenados no **BigQuery**

- Histórico transacional
- Balanços financeiros
- Dados cadastrais das empresas

### 📄 Dados Não Estruturados

- Trocas de **e-mails**
- **Contratos sociais em PDF**
- **Notícias de mercado**

### 📦 Volume de processamento


### 🎯 Objetivo

Construir um sistema capaz de:

- Automatizar decisões de crédito
- Gerar **justificativas explicáveis**
- Minimizar **risco financeiro e operacional**
- Garantir **compliance e governança de dados**

---

# 🏗️ O Desafio Arquitetural

A solução deve ser projetada **end-to-end na Google Cloud Platform**.

---

# 📦 Parte 1 — Arquitetura Híbrida e Qualidade de Dados

Desenhar a solução técnica completa contemplando ingestão, processamento e inferência.

## 🔄 Pipeline de Ingestão e Qualidade de Dados

Antes que os dados cheguem ao modelo ou à **Feature Store**, é necessário garantir qualidade.

Definir:

- Validação de **schema**
- **Data contracts**
- Detecção de **data drift**
- Regras de qualidade

### ❓ Pergunta crítica

O que acontece se um **dado transacional estiver corrompido**?

A arquitetura deve prever:

- isolamento do dado
- alertas
- fallback seguro

---

## ⚙️ O Motor de Risco (ML Clássico)

Projetar a arquitetura para o cálculo do **score de risco numérico**.

Justificar o uso de modelos determinísticos como:

- **XGBoost**
- **Scikit-learn**

em vez de LLMs para essa etapa.

Critérios esperados:

- explicabilidade
- estabilidade
- eficiência computacional
- auditabilidade

---

## 🤖 O Agente de Contexto (GenAI)

Arquitetura responsável por extrair conhecimento de dados não estruturados.

Exemplos:

- análise de contratos
- análise de e-mails
- análise de notícias de mercado

O objetivo é gerar **sinais contextuais que complementam o modelo de risco**.

---

# 🔐 Parte 2 — Segurança e Privacidade (Security by Design)

Os documentos analisados podem conter **dados sensíveis (PII)**.

### Exemplos de PII

- Nomes
- CPF
- Endereços
- Dados bancários
- Informações financeiras

---

## 🛡️ Proteção de PII

Definir como garantir que dados sensíveis:

- não sejam expostos indevidamente
- não sejam enviados diretamente ao modelo GenAI
- não vazem em logs

---

## 🔎 Estratégias esperadas

Implementar:

### 🔒 Ofuscação e Redação de Dados

Exemplo de ferramentas:

- **DLP (Data Loss Prevention)**

Técnicas:

- Masking
- Tokenização
- Redação automática

---

### 🧩 Controles de acesso

Definir políticas usando:

- **IAM**
- **VPC Service Controls**

Objetivos:

- isolamento de dados
- proteção contra exfiltração
- compliance regulatório

---

# 🤝 Parte 3 — Orquestração A2A (Agent-to-Agent)

Projetar como os agentes interagem entre si.

---

## 🔄 Interação entre Agentes

Criar um fluxo onde:

- **Agente de Risco (Numérico)** calcula o score
- **Agente de Contexto (Textual)** analisa documentos

Ambos colaboram para produzir a decisão final.

---

## 📈 Diagrama de Sequência

O diagrama deve mostrar:

1️⃣ Solicitação de crédito  
2️⃣ Análise do modelo de risco  
3️⃣ Extração de contexto textual  
4️⃣ Consolidação da decisão  
5️⃣ Geração da justificativa

---

## 🚨 Tratamento de Falhas

Exemplo: Falha no OCR do contrato PDF


O sistema deve decidir entre:

- negar automaticamente
- solicitar revisão humana
- reprocessar o documento

Definir claramente o **protocolo de fallback**.

---

# 💰 Parte 4 — FinOps e Engenharia de Custos

Existe **restrição orçamentária**.

A arquitetura precisa ser economicamente viável.

---

## ⚖️ Trade-off de Custos

Demonstrar matematicamente a diferença de custo entre:

### Abordagem 1 — GenAI puro
100% das requisições processadas via Gemini 1.5 Pro


### Abordagem 2 — Arquitetura híbrida
- Triagem inicial com **XGBoost**
- Apenas casos **cinzentos** enviados ao LLM

Fluxo esperado:
XGBoost → triagem inicial
↓
Casos simples → decisão automática
↓
Casos cinzentos → Gemini Flash / Gemini Pro


Calcular:

- custo diário
- custo mensal
- economia obtida

---

# 🧠 Parte 5 — Governança e Grounding

Um sistema de crédito **não pode gerar justificativas inventadas**.

---

## 🚫 Prevenção de Alucinação

Explicar como implementar **RAG (Retrieval-Augmented Generation)**.

O modelo deve gerar respostas **baseadas em evidências reais**.

---

## 🔎 Grounding baseado em dados

A justificativa precisa vir de dados verificáveis, 
por exemplo: "Negado por dívida ativa registrada em órgão regulador".


E não por inferências do modelo.

---

## 🧩 Integração com Feature Store

O RAG deve recuperar informações como:

- histórico de inadimplência
- dívidas registradas
- indicadores financeiros

Essas informações alimentam o prompt do modelo para gerar **explicações auditáveis**.

---

# 🏁 Resultado Esperado

Uma arquitetura que combine:

✅ **Machine Learning clássico**  
✅ **GenAI contextual**  
✅ **Segurança e privacidade**  
✅ **Governança de IA**  
✅ **Controle de custos (FinOps)**  
✅ **Escalabilidade na GCP**

---

# 🚀 Objetivo Final

Construir um sistema de decisão de crédito que seja:

- **Inteligente**
- **Explicável**
- **Seguro**
- **Escalável**
- **Economicamente sustentável**

