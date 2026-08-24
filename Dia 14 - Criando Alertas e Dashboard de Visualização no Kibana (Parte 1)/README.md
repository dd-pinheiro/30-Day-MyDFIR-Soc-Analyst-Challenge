# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 14

---

## 🎯 Objetivo do Dia
Configurar regras de alerta e estruturar visualizações em dashboards no **Kibana** para detectar e monitorar de forma automatizada as tentativas de Brute Force via SSH

---

## Atividades Práticas Realizadas
### 1) **Identificação de Padrões no Kibana Discover:**
1. Acesse a interface do Kibana e navegação até a seção **Discover** e utilizando a seguinte query para pesquisa no KQL:
`system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Failed` 
2. Logo em seguida, selecione os campos que informam aspectos relevantes para melhor analise diante de uma tentativa de brute force, tais como `host.ip`, `message`, `user.name` e `source.ip`.
Por fim, sua query deve ficar da seguinte forma:
<img width="1153" height="729" alt="image" src="https://github.com/user-attachments/assets/069b2707-ff6f-4cf4-b7a9-9dd4b5508257" />

### 2) **Criação de Dashboard**
   1. Va até a aba "Maps" e coloque a query utilizada no **Passo 1**.
   2. Pesquise pela query e logo em seguida selecione "**Add Layer**"
   3. O mapa de visualização varia de acordo com sua escolha, mas como demonstração utilizei o mapa *Choropleth*, que demarca as áreas geográficas de acordo com o *Threshold* do alerta.
   4. Salve as alterações e crie um novo dashboard.
   5. Crie um plano de visualização tanto para logins bem sucedidos quanto para tentativas de brute force SSH que tiveram falha. Por último, salve novamente as suas alterações; e finalmente você terá seu dashboard de visualização para atividades SSH:
<img width="1436" height="334" alt="image" src="https://github.com/user-attachments/assets/81052ee6-4188-4392-9f09-19816e3b3da8" />


---

## Consultas e Parâmetros Úteis (KQL / Kibana)
Durante a criação e validação das regras de detecção, foram aplicados filtros e estruturas como:

* **Filtrar falhas de autenticação SSH:**
  `system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Failed`
* **Filtrar Autenticação bem sucedida via SSH:**
  `system.auth.ssh.event : * and agent.name: myDFIR-Ubuntu-SSH-Server and system.auth.ssh.event: Accepted`

Vale ressaltar que campo `agent.name` varia de acordo com o hostname de seu servidor.


  
