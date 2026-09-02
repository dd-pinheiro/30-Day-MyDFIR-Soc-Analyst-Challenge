# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 16

---

## 🎯 Objetivo do Dia
Estender a criação de threshold de alertas e monitoramento para o ambiente **Windows Server** no Elasticsearch, focando na detecção de tentativas de login falhas via RDP (`Event ID 4625`).

---

## Atividades Práticas realizadas
### 1) **Filtros e Análise de Logs do Windows no Discover:**
1. No Kibana, fui até a aba "Discover" e utilizei a seguinte query para pesquisar por falhas de autenticação via RDP utilizando a linguagem KQL:
`event.code: 4625 and agent.name: "BobServer"`
Vale ressaltar que o campo `agent.name` varia de acordo com o hostname de seu servidor.

2. Logo em seguida, selecionei os campos que informam aspectos relevantes para melhor analise diante de uma tentativa de brute force (por exemplo, `user.name`, `source.IP`, `source.geo.contry_name`)
3. Salvei as alterações em "**Save**" localizado no canto superior direito
4. Após salvar a query, criei um novo Alerta realizando os passos enumerados na imagem abaixo:
<img width="1181" height="666" alt="image" src="https://github.com/user-attachments/assets/1a690823-8235-4072-8f9c-416d2cdc2491" />

### 2) Criando regra de brute force SSH via SIEM
1. Fui até a aba de **Security**, selecionei **Rules** e logo em seguida selecionei **Detection Rules (SIEM)**.
2. Nessa aba, criei uma nova regra em "**Create New Rule**" e coloquei a Query Customizada de falhas de falhas de login SSH utilizada no **Dia 14**, mas adicionei na query o campo `user.name: root`. O restante dos campos, preenchi da seguinte forma:
<img width="1113" height="581" alt="image" src="https://github.com/user-attachments/assets/c387f890-0d98-4b4c-9c21-ac89bff74df1" />
Prossiga clicando em "Continue".

4. Na aba de "**About rule**", será necessário realizar algumas mudanças em relação ao alerta; os campos que alterei foram os campos **Name, Description, Default Severity** e **Custom highlighted fields**. 
5. Na aba de "**Schedule Rule"**, coloquei ambos os campos para dar trigger de 5 em 5 minutos; e não habilitei nenhuma ação para regra (ainda).
6. Por fim criei e habilitei a regra em "**Create & enable rule**""

### 3) Criando regra de brute force RDP via SIEM
Realizei os mesmo passos feito em **2)**, porém utilizei uma query para pesquisa de brute-force via RDP, ou seja, outra Query KQL será utilizada:
```
    event.code: 4625 and agent.name: "BobServer" and user.name: "Administrator"
```
Note que essa regra especifica o Event ID 4625 (Falha de autenticação via RDP) no servidor BobServer utilizando o usuário *Administrator*. Ou seja, essa regra irá gerar um alerta sempre que esses três critérios forem "ativados"; caso contrário, não irá gerar um alerta.

---

## Resultado
No final, duas regras devem ser criadas para serem monitoradas através do SIEM:
<img width="1186" height="91" alt="image" src="https://github.com/user-attachments/assets/cbf36623-d043-4e41-820f-0edc86ec37cd" />

---

## Consultas e Filtros Úteis (KQL)
Durante a configuração no Discover e nas regras de SIEM, foram utilizados filtros como:

* **Filtrar tentativas de login falhas no Windows (Event ID 4625):**
  ```kql
  agent.name: "<NOME_DO_AGENT_WINDOWS>" AND event.code: "4625"

---

## 💡 Lições Aprendidas
- Criação de Regras via SIEM para detecção de Brute Force SSH/RDP
- Pesquisa avançada de Query, envolvendo hosts específicos e atividades especificas.
