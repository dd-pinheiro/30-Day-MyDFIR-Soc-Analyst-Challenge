# 🛡️ 30-Day SOC Analyst Challenge - Day 27

---

## 🎯 Objetivo do Dia
De forma similar ao dia 26, o objetivo deste dia foi investigar os alertas de força bruta via RDP no painel de SIEM do Elastic Security, envolvendo triagem do alerta; a determinação da natureza maliciosa do IP de origem, a identificação das contas de usuário alvo, a verificação de eventuais tentativas de autenticação bem-sucedidas e a documentação ou resolução adequada do alerta utilizando osTicket.

Essa documentação será bem similar à que foi feita no dia anterior, a única diferença aqui é que será feita a análise do protocolo RDP.

--- 

### Investigação
Da mesma forma que realizamos a análise de ataque de força bruta via SSH no **Dia 26 - Investigando Ataques de Força Bruta via SSH**, realizaremos também a analise de ataque de força bruta via RDP, porque mesmo sendo protocolos diferentes, a mesma metodologia pode ser utilizada:
- Analise o IP de origem - Ele é conhecido como malicioso?
- Há outros usuários que estão sendo afetados por este IP?
- Algumas dessas tentativas de *Brute-Force* via RDP foi bem-sucedida?
- Se sim, que tipo de atividade ocorreu após esse usuário efetuar login?

Antes de começar, vá até até a aba **Security** no Elastic search > selecione **Alerts** e filtre pelo alerta de brute força via RDP.
<img width="1431" height="765" alt="image" src="https://github.com/user-attachments/assets/e4700b5e-7b1e-46c3-bd47-81df0a36c8b1" />

### Analise o IP de origem - Ele é conhecido como malicioso?
Como demonstração, utilizei o IP *185.118.79.103* e o pesquisei no AbuseIPDB [https://www.abuseipdb.com]
<img width="1641" height="819" alt="image" src="https://github.com/user-attachments/assets/16f812c8-3105-4113-8b98-e2dfc608ba84" />

Diante das informações de Threat Intelligence nos sites acima, posso afirmar que o IP 91.92.40.200 é considerado um IP malicioso, contendo registros de Brute force SSH; Port Scan e Hacking.

### Há outros usuários que estão sendo afetados por este IP?
Utilizando a aba de Discover no Elasticsearch, utilize uma query personalizada com o intuito de pesquisar se outros usuários estão sendo afetados por este mesmo IP
<img width="1385" height="716" alt="image" src="https://github.com/user-attachments/assets/6fec78b1-5394-410f-b5d1-dec58a72202a" />

Neste caso a resposta é sim, os usuários *Admin* e *User* também estão sendo afetados pelo IP *185.118.79.103*

### Algumas dessas tentativas de *Brute-Force* via RDP foi bem-sucedida?
Novamente, na aba Discover pesquise utilizando uma query que mostra se algumas dessas tentativas de Brute-Force foi bem-sucedida. No exemplo abaixo, note que utilizei o campo `event.code: 4624`, que de forma resumida, é o evento gerado caso um usuário consiga se autenticar com sucesso ao servidor através do protocolo RDP.
<img width="1342" height="713" alt="image" src="https://github.com/user-attachments/assets/1b7285a6-9d5a-4e6a-8a55-d585cca4ad23" />

Como não obtive nenhum resultado na minha, posso afirmar que até o momento ninguém conseguiu executar o ataque de Força bruta com sucesso ao meu servidor Windows.

### Se sim, que tipo de atividade ocorreu após esse usuário efetuar login?
Essa pergunta é complementar à pergunta *Algumas dessas tentativas de Brute-Force via SSH foi bem-sucedida?. Basicamente, uma análise mais detalhada será necessária caso identifique que uma ou mais dessas tentativas de Brute-force via RDP foi bem sucedida. Procure por informações relevantes, tais como:
- Algum Script foi baixado após o login?
- Eles utilizaram um comando de reconhecimento (`ipconfig` `hostname`, `netstat`, `whoami`)?
- Eles executaram algum comando malicioso?

---

## Gerando Tickets no osTicket de forma automatizada.
Nessa parte, criei uma ação para cada vez que um alerta for gerado, um ticket será criado no osTicket.
1. Em "**Rules**" > **Detection Rules (SIEM)**, também localizada em *Security*; selecionei a regra de *Brute-Force via RDP*.
2. Em "**Edit Rule Settings**" > **Actions** > Selecionei o webhook; note que o conector criado no **Dia 25 - Integração ELK Stack e osTicket** já está pré-selecionado. A única coisa que precisei mudar é o campo "Body", que irá conter as informações do ticket:
```
   <?xml version="1.0" encoding="UTF-8"?>
<ticket alert="true" autorespond="true" source="API">
    <name>Elasticsearch</name>
    <email>bananaSecurity@gmail.com</email>
    <subject>{{rule.name}}</subject>
    <phone>11 70707-7070</phone>
    <message type="text/plain"><![CDATA[Alert: {{rule.name}}
    Source IP: {{context.alerts.0.source.ip}}
    Username: {{context.alerts.0.user.name}}
    Severity: {{context.rule.severity}}
    
    Link to investigate the rule:
    {{rule.url}}]]></message>
</ticket>
```
<img width="1041" height="701" alt="image" src="https://github.com/user-attachments/assets/e90471b7-d78e-458e-b34f-09af99c0aafe" />

Os campos que estão com chaves; por exemplo `{{rule.name}}`, são variáveis que puxam informações especificas dependendo da regra. Para obter mais informações sobre essas variáveis, visite a documentação oficial do Elasticsearch em [https://www.elastic.co/docs/explore-analyze/alerting/alerts/rule-action-variables] 

A variável `{{rule.url}}` é um link que leva o Técnico/analista que irá analisar o ticket direto para o Alerta que gerou esse ticket, dessa forma facilita ainda mais o processo de triagem do Incidente.

<img width="549" height="734" alt="image" src="https://github.com/user-attachments/assets/9e34ac26-2db9-4344-89f1-d2598df2f776" />

---

## 📷 Capturas de Tela

Abaixo, segue a captura de tela de um dos tickets que foram gerados por conta do Alerta que foi configurado:

<img width="927" height="646" alt="image" src="https://github.com/user-attachments/assets/9442f7ac-42b5-4c71-ac83-06d789b1266a" />

Abaixo, segue mais uma captura de tela de todos os tickets que foram gerados em relação aos Alertas de Brute-Force RDP:

<img width="902" height="761" alt="image" src="https://github.com/user-attachments/assets/9066cc68-df38-44e5-9f37-f0add2c3e26f" />


Esse volume abundante de ticket é feito propositalmente, afinal estamos em um ambiente de testes e o propósito dele é aprender como um sistema de Tratamento de Tickets e resposta a incidentes funciona.
Além disso, vale ressaltar, que antes de começar a tratativa de um ticket, sempre dê um "Assign" e o coloque em seu nome, assim você evitará que outra pessoa comece a tratar o mesmo ticket que você está tratando.

---

## 💡 Lições Aprendidas
- Análise de Alertas de Brute-force via RDP
- Metodologia de Triagem: Sempre cheque o IP de Origem, quais usuários foram afetados; se alguma tentativa obteve sucesso; se sim, quais foram as ações feitas após o login


