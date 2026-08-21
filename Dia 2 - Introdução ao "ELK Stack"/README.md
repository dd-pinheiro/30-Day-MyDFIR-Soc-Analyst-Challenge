# 🛡️ 30-Day SOC Analyst Challenge - Day 2

## 🎯 Objetivo do Dia
Compreender a arquitetura do **ELK Stack (Elasticsearch, Logstash e Kibana)** e o papel fundamental do monitoramento de segurança e da coleta de telemetria em um ambiente SOC.

---

## 🏗️ O que é o ELK Stack?
O ELK Stack é uma plataforma centralizada de gerenciamento de logs e análise de dados em tempo real, muito utilizada como SIEM (Security Information and Event Management), composta por três ferramentas principais:

1. **Elasticsearch:** 
   - Realiza a busca e análise.
   - Responsável por armazenar, indexar e permitir buscas rápidas em grandes volumes de dados usando APIs RESTful e JSON.
2. **Logstash:** 
   - Coleta dados de várias fontes, filtra, transforma e os envia limpos para o Elasticsearch.
3. **Kibana:** 
   - A interface web de visualização e exploração de dados.
   - Permite criar dashboards, painéis de monitoramento, investigações via console e triggers de alerta.

## 📋 Aprendizado:
* **Correlação de Eventos:** Um único log isolado raramente conta a história toda; o SIEM permite correlacionar eventos de diferentes fontes (ex: Firewall + Windows Event Logs) para expor um ataque real.
* **Beats / Elastic Agent:** Agentes leves instalados em endpoints para coletar métricas, tráfego de rede e logs de segurança.
* **Sysmon (System Monitor):** Ferramenta essencial da Microsoft Sysinternals para capturar telemetria avançada de eventos no Windows (criação de processos, conexões de rede, alterações no registro).

---
