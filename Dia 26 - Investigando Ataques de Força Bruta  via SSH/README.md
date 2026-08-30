# 🛡️ 30-Day SOC Analyst Challenge - Day 26

---

## 🎯 Objetivo do Dia
O objetivo deste dia é investigar um alerta de força bruta via SSH no painel de SIEM do Elastic Security. Essa investigação envolve a triagem do alerta, a determinação da natureza maliciosa do IP de origem, a identificação das contas de usuário alvo, a verificação de eventuais tentativas de autenticação bem-sucedidas e a documentação ou resolução adequada do alerta utilizando osTicket.

---

## Investigação
Para começar a investigação de seus alertas, vá até a aba "**Security**" e selecione "**Alerts**".
<img width="1411" height="756" alt="image" src="https://github.com/user-attachments/assets/7c0d20b1-ddc7-4652-9d0e-33a7fba7d365" />

Neste caso, como nosso objetivo principal é investigar alertas de Ataque de Brute-force via SSH, devemos sempre nos questionarmos sobre o que será analisado primeiramente. Abaixo, segue alguns pontos importantes para serem observados ao analisar este tipo de alerta:
- Analise o IP de origem - Ele é conhecido como malicioso?
- Há outros usuários que estão sendo afetados por este IP?
- Algumas dessas tentativas de *Brute-Force* via SSH foi bem-sucedida?
- Se sim, que tipo de atividade ocorreu após esse usuário efetuar login?

Abaixo, vou demonstrar como "obter" de certa forma a resposta para essas perguntas.

### Analise o IP de origem - Ele é conhecido como malicioso?
Você pode identificar essa informação através de diversos sites de Threat Intelligence, mas os que eu mais utilizo para este tipo de analise são:
- [https://www.abuseipdb.com/]
- [https://www.greynoise.io/]

Diante das informações de Threat Intelligence nos sites acima, posso afirmar que o IP 91.92.40.200 é considerado um IP malicioso, contendo registros de *Brute force SSH; Port Scan; Bots; Hacking*
<img width="1896" height="937" alt="image" src="https://github.com/user-attachments/assets/4b8f72e1-a5b0-4941-94bc-807575b3a2cd" />

### Há outros usuários que estão sendo afetados por este IP?
Utilizando a aba de *Discover* no Elasticsearch, utilize uma query personalizada com o intuito de pesquisar se outros usuários estão sendo afetados por este mesmo IP. Com o intuito de facilitar a visualização, inseri a coluna `user.name` na tabela e na *query*:
<img width="1426" height="692" alt="image" src="https://github.com/user-attachments/assets/bdd60185-db29-4c79-b291-0d10868fc6d7" />

Na captura de tela, você claramente consegue verificar que outros usuários também estão sendo afetados pelo Ataque de Força bruta.

### Algumas dessas tentativas de *Brute-Force* via SSH foi bem-sucedida?
Novamente, na aba *Discover* pesquise utilizando uma query que mostra se algumas dessas tentativas de Brute-Force foi bem-sucedida:
<img width="1352" height="668" alt="image" src="https://github.com/user-attachments/assets/745b6de3-4154-4f96-b43a-8eccbdb3f1db" />

Como não obtive nenhum resultado na minha, posso afirmar que até o momento ninguém conseguiu executar o ataque de Força bruta com sucesso ao meu servidor.

### Se sim, que tipo de atividade ocorreu após esse usuário efetuar login?
Essa pergunta é complementar à pergunta *Algumas dessas tentativas de *Brute-Force via SSH foi bem-sucedida?*. Basicamente você irá realizar uma analise mais detalhada caso identifique que alguma dessas tentativas de Brute-force via SSH foi bem sucedida. Em casos como esse procure:
- Algum Script foi baixado após o login?
- Eles utilizaram um comando de *reconhcimento* (`whoami`,`ip a`, `hostname`, `netstat`)?
- Eles executaram algum comando malicioso?

Existem outras analises que devem ser feitas, mas não citarei todas pois não quero estender esse tema mais que o necessário.

---

## Gerando Tickets no osTicket de forma automatizada.
Nessa parte, iremos fazer com que nossos alertas gerem tickets no osTicket.
1. Vá até a aba "**Rules**" > **Detection Rules (SIEM)**, também localizada em *Security*; selecione a sua regra de *Brute-Force via SSH*.
2. Clique em "**Edit Rule Settings**" > **Actions** > Selecione o webhook; note que o nosso conector criado no **Dia 25 - Integração ELK Stack e osTicket** já está pré-selecionado. A única coisa que precisamos mudar é o campo "Body", que irá conter as informações do ticket:
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
Os campos que estão com chaves; por exemplo `{{rule.name}}`, são variáveis que puxam informações especificas dependendo da regra. Para obter mais informações sobre essas variáveis, visite a documentação oficial do Elasticsearch em [https://www.elastic.co/docs/explore-analyze/alerting/alerts/rule-action-variables] 

A variável `{{rule.url}}` é um link que leva o Analista que irá analisar o ticket direto para o Alerta que gerou esse ticket, dessa forma ficará mais fácil de analisar o que causou gerou o ticket sem precisar procurar manualmente na aba Alertas do SIEM.

---

## 📷 Capturas de Tela:
Abaixo, segue a captura de tela de um dos tickets que foram gerados por conta do Alerta que foi configurado:
<img width="931" height="758" alt="image" src="https://github.com/user-attachments/assets/4261fb18-4759-4427-b2e7-bb238118415b" />

Abaixo, segue mais uma captura de tela de todos os tickets que foram gerados em relação aos Alertas de Brute-Force SSH:
<img width="931" height="758" alt="image" src="https://github.com/user-attachments/assets/3b06fa22-df44-4689-af13-33ad8b108d53" />

Esse volume abundante de ticket é feito propositalmente, afinal estamos em um ambiente de testes e o propósito dele é aprender como um sistema de Tratamento de Tickets e resposta a incidentes funciona.
Além disso, vale ressaltar, que antes de começar a tratativa de um ticket, sempre dê um "Assign" e o coloque em seu nome, assim você evitará que outra pessoa comece a tratar o mesmo ticket que você está tratando.

Na captura de tela abaixo, demonstro com o seria feita a resolução de um desses tickets.
<img width="711" height="702" alt="image" src="https://github.com/user-attachments/assets/2db4a844-f973-4f5e-9bc0-fda33c2e5eb9" />

---

## 💡 Lições Aprendidas
- Metodologia de Triagem: Sempre cheque o IP de Origem, quais usuários foram afetados; se alguma tentativa obteve sucesso; se sim, quais foram as ações feitas após o login
- Utilizar plataformas de *Threat Intelligence* para obter informações.
- Adicionando uma ação a uma regra para gerar Tickets no osTicket.

