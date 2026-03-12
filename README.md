# azure-application-platform-architecture
Projeto de Arquitetura Cloud na Azure. Desenho de infraestrutura para um CRM Imobiliário utilizando App Service, Kubernetes (AKS), API Management e Azure Functions (Serverless).

# ☁️ Microsoft Application Platform: Arquitetura Cloud para CRM Imobiliário

Este repositório documenta o projeto final do módulo "Microsoft Application Platform" do bootcamp da Digital Innovation One (DIO). O objetivo é demonstrar a integração de múltiplos serviços gerenciados da Azure para sustentar uma aplicação complexa, segura e escalável.

> **Nota de Arquitetura:** O desenho abaixo reflete a infraestrutura em nuvem ideal para um **Sistema de Vendas e Gestão Imobiliária** (CRM), abordando desde a hospedagem do front-end até o processamento assíncrono de contratos.

## 🎯 Objetivo do Projeto
Projetar uma arquitetura de microsserviços na nuvem Microsoft Azure, aplicando conceitos de conteinerização, segurança de borda (edge security) e computação serverless para garantir alta disponibilidade e otimização de custos.

## 🏗️ Desenho da Solução

A infraestrutura foi dividida em 4 pilares principais, cada um utilizando o melhor serviço da Azure para a sua função:

1. **Front-end e Web App (Azure App Service):**
   * Hospedagem da interface do usuário (ex: um painel em Python/Streamlit ou React).
   * **Vantagem:** Facilidade de deploy (CI/CD) e escalabilidade automática conforme o tráfego de corretores acessando o sistema.

2. **Gerenciamento de APIs (Azure API Management - APIM):**
   * Atua como o *API Gateway* (proxy reverso) do sistema.
   * **Vantagem:** Protege os dados sensíveis dos clientes e imóveis, aplicando limites de requisições (Rate Limiting) e exigindo chaves de assinatura (Subscription Keys).

3. **Backend em Microsserviços (Azure Kubernetes Service - AKS):**
   * Onde roda a regra de negócio pesada (gerenciamento de anúncios, regras de comissão, etc.) isolada em contêineres Docker (Pods).
   * **Vantagem:** Orquestração gerenciada, permitindo escalar apenas os serviços que estão sob estresse.

4. **Processamento Assíncrono (Azure Functions):**
   * Computação *Serverless* ativada por gatilhos (Triggers).
   * **Casos de Uso no CRM:** Quando um imóvel é vendido, uma *Azure Function* é disparada para gerar o contrato em PDF (salvando no Blob Storage) e enviar um e-mail de notificação aos envolvidos, sem travar a tela do usuário.

## 💡 Insights e Aprendizados
* **Desacoplamento:** Aprendi que separar o front-end (App Service) das APIs (APIM/AKS) aumenta drasticamente a resiliência do sistema. Se a interface cair, as integrações de API continuam funcionando.
* **Custo-Benefício:** O uso de *Azure Functions* no plano de Consumo para tarefas esporádicas (como gerar relatórios de fim de mês) evita manter servidores caros rodando 24 horas por dia.
* **Segurança Integrada:** A combinação de APIM na borda com Identidades Gerenciadas (Managed Identities) no backend garante que os serviços conversem entre si sem a necessidade de expor senhas no código.

## 🚀 Próximos Passos
Como evolução técnica desta infraestrutura, planejo incorporar serviços de IA Generativa para criar descrições automáticas de imóveis com base em fotos, além de otimizar a camada de persistência utilizando Azure SQL Database.
