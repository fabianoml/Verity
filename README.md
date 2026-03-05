# Verity
Desafio Verity

Desafio Técnico: O "Analista de Crédito Híbrido" 
Contexto do Cenário 
Uma instituição financeira digital (GCP First) está automatizando a concessão de crédito para 
PMEs. O processo envolve: 
Dados Estruturados: Histórico transacional, balanços e dados cadastrais no BigQuery. 
Dados Não Estruturados: Trocas de e-mails, contratos sociais em PDF e notícias de 
mercado. Volume: 10.000 pedidos/dia.  
Meta: Decisão automática com justificativa, minimizando o risco financeiro e 
operacional. 
O Desafio Arquitetural 
Parte 1: Arquitetura Híbrida e Qualidade de Dados (Data Quality)  
Desenhe a solução técnica ponta a ponta na GCP, detalhando: 
● Pipeline de Ingestão e Qualidade: Antes de os dados chegarem ao modelo ou à 
Feature Store, como você garante a qualidade? Defina onde entram validação de 
schema, detecção de data drift e data contracts. O que acontece se o dado transacional 
estiver corrompido? 
● O Motor de Risco (ML Clássico): Arquitetura para o cálculo do score numérico. 
Justifique o uso de modelos determinísticos (XGBoost/Scikit-learn) versus LLMs para 
esta etapa. 

● O Agente de Contexto (GenAI): Arquitetura para extração de dados não estruturados. 
Parte 2: Segurança e Privacidade (Security by Design)  
Os e-mails e contratos contêm dados sensíveis (PII - Nomes, CPFs, Endereços, Sigilo 
Bancário). 
● Proteção de PII: Como você garante que dados sensíveis não sejam expostos 
indevidamente ao modelo de GenAI ou vazados nos logs? 
● Descreva a estratégia de ofuscação/redação (ex: DLP) e controles de acesso (IAM/VPC 
Service Controls) que você implementaria para garantir compliance. 
Parte 3: Orquestração A2A (Agent-to-Agent)  
Projete o fluxo de interação entre os componentes. 
● Desenhe um diagrama de sequência mostrando como o Agente de Risco (Numérico) e 
o Agente de Contexto (Textual) colaboram. 
● Como o sistema lida com falhas? (Ex: O serviço de OCR do PDF falhou, o modelo de 
risco deve negar o crédito ou pedir revisão humana?). Defina o protocolo de fallback. 
Parte 4: FinOps & Engenharia de Custos  
Você tem um orçamento restrito. 
● Trade-off: Demonstre matematicamente (estimativa) a diferença de custo mensal entre 
processar todas as 10.000 requisições/dia via Gemini 1.5 Pro versus uma abordagem 
híbrida (XGBoost para triagem inicial + Gemini Flash/Pro apenas para casos cinzentos). 
● Justifique a viabilidade econômica da sua escolha. 
Parte 5: Governança e Grounding 
● Prevenção de Alucinação: Explique como utilizará técnicas de RAG 
(Retrieval-Augmented Generation) conectadas à Feature Store para garantir que a 
justificativa da recusa seja baseada em fatos reais (ex: "Negado por dívida ativa em X") 
e não em invenções do modelo.
