# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 14

---

## 🎯 Objetivo do Dia
Investigar e validar a ingestão bem-sucedida dos logs do servidor Ubuntu no SIEM, criando consultas no **Kibana Discover** para analisar os ataques de força bruta SSH em tempo real e visualizar os dados consolidados.

---

## 🛠️ Atividades Práticas Realizadas
1. **Acesso ao Kibana Discover:**
   * Navegação até o painel **Discover** do Elastic Stack para explorar os dados brutos enviados pelo Elastic Agent instalado no servidor Ubuntu.
   * Seleção da *Data View* correta para filtrar os logs do sistema operacional (`auth.log`).

2. **Filtros e Consultas de Logs (KQL):**
   * Aplicação de filtros utilizando a *Kibana Query Language (KQL)* para isolar eventos específicos de falhas de autenticação.
   * Identificação de campos essenciais gerados pelos logs do Linux, como nome de usuário tentado, IP de origem e status da autenticação.

3. **Análise de Indicadores de Ataque:**
   * Verificação visual dos picos de requisições maliciosas vindas de diferentes partes do mundo contra a porta SSH exposta da máquina virtual.

---

## 💻 Consultas e Filtros Úteis (KQL)
Durante a exploração no Discover, alguns filtros no formato KQL foram aplicados para refinar a busca:

* **Filtrar apenas tentativas de login falhas:**
  ```kql
  event.action : "failed" or message : "*Failed password*"
