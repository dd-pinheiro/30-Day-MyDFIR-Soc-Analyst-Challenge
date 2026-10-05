# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 14

---

## 🎯 Objetivo do Dia
Configurar regras de alerta e estruturar visualizações em dashboards no **Kibana** para detectar e monitorar de forma automatizada as tentativas de Brute Force via SSH

---

## Atividades Práticas Realizadas
### 1) **Identificação de Padrões no Kibana Discover:**
1. Fui até a seção **Discover** no Elasticsearch e no campo de pesquisa, inseri a seguinte Query utilizando a linguagem KQL:
`system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Failed` 
2. Logo em seguida, selecionei os campos que informam aspectos relevantes para melhor analise diante de uma tentativa de brute force, tais como `host.ip`, `message`, `user.name` e `source.ip`.
3. Após pesquisar a query e selecionar os campos necessários, criei um Alerta, clicando em "**Alerts**" > "**Create search threshold rule**":
<img width="1186" height="826" alt="image" src="https://github.com/user-attachments/assets/46993f8f-ec25-45bb-b1a3-bf3fbceb7510" />

### 2) **Criação de Dashboard**
   1. Na aba "**Maps**" pesquisei pela query utilizada no **Passo 1**: `system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Failed` 
   2. Selecionei a opção de "**Add Layer**"
   3. O mapa de visualização varia de acordo com sua escolha, mas por fins demonstrativos, utilizei o mapa *Choropleth*, que demarca as áreas geográficas de acordo com o *Threshold* do alerta.
   4. Após configurar o mapa, salvei as alterações e criei um novo dashboard.
   5. Assim como criei um mapa para falhas de login SSH, também criei um mapa para logins bem sucedidos via SSH, dessa forma ficará mais fácil realizar a análise de quem está acessando o sistema e quem tem acesso ao sistema.
<img width="1436" height="334" alt="image" src="https://github.com/user-attachments/assets/81052ee6-4188-4392-9f09-19816e3b3da8" />

---

## Consultas e Parâmetros Úteis (KQL / Kibana)
Durante a criação e validação das regras de detecção, foram aplicados filtros e estruturas como:

* **Filtrar falhas de autenticação SSH:**
  `system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Failed`
* **Filtrar Autenticação bem sucedida via SSH:**
  `system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Accepted`

Vale ressaltar que campo `agent.name` varia de acordo com o hostname de seu servidor.

---

## 💡 Lições Aprendidas
- Pesquisa de query utilizando a linguagem KQL
- Criando regras de threshold no Kibana
- Criação de mapas e Dashboards

  
