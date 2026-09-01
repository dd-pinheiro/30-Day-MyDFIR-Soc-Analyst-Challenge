# 🛡️ 30-Day SOC Analyst Challenge - Day 28

---

## 🎯 Objetivo do Dia
- Identificar atividades relacionadas ao agente do Mythic C2, buscando o payload executado do Mythic;
- Correlacionando telemetria analisando logs do Sysmon (Event ID 1, 3 e 29);
- Integração com osTicket: Configurar ações de Webhook no SIEM para enviar criação automática de tickets.

---

## Introdução
Antes de começar, vale ressaltar alguns pontos:

Vale ressaltar que nesse laboratório, nomeei o payload de `payload.exe`.


Mas fica aqui um questionamento, ***Como posso investigar de uma forma mais detalhadas as atividades do Mythic?*** A forma mais comum é através de Telemetria de redes (Network Telemetry) e Investigação de Criação de Processos (Event ID 1); abaixo descreverei brevemente cada um desses dois:

#### Network Telemetry
Normalmente, quando existe alguma sessão ativa de **Command & Control** em um computador, acaba gerando muito tráfico de *Inbound* e *Outbound*, o que significa que múltiplos *bytes* estão sendo transmitidos entre o Servidor de Command & Control e a máquina alvo. O resultado disso é diversas logs sendo geradas de comunicação entre esses dois hosts.

#### Investigando "Process Creation (Event ID 1)"
Além de pesquisar por Network Telemetry (Event ID 3), uma boa prática é procurar por Process Creation (Event ID 1). No entanto, não vou mostrar a query de pesquisa, mas sim o Dashboard feito no **Dia 22 - Criação de regra de threshold para atividades do Mythic e criação de Tabela detalhada**, que mostra de forma "tabular" os Events ID's 1 e 3:
<img width="1430" height="677" alt="image" src="https://github.com/user-attachments/assets/adb78b7d-bd7e-40c5-a306-6657f45e5c76" />

Através desses dois dashboards criados, fica mais fácil de correlacionar os eventos gerados pelo Mythic.

---

## Investigação 
Pesquisando pelo nome do payload (`payload.exe`) na aba de *Discover* do Elastic, obtenho os seguitnes resultados: 
<img width="1200" height="514" alt="image" src="https://github.com/user-attachments/assets/f2ed247b-4940-4459-847d-43710fdfbedc" />

No entanto, meu objetivo é verificar as atividades relacionados aos Event ID's 3 e 1 na máquina, então utilizei meu dashboard criado:
<img width="1379" height="466" alt="image" src="https://github.com/user-attachments/assets/deeb368b-888e-4f84-8686-23e225c27fec" />

Note que encontrei uma logs de **Event ID 3 - Network Connection (Remote)** na tabela, em um cenário real, eu me questionaria:
- Porque tem um executável iniciando uma conexão remota?
- Que tipo de endereço de IP de destino é esse?
- Porque está utilizando a porta HTTPS (443)?

Fazendo uma análise mais detalhada desse executável, fiz um *threat hunting*

1. Na aba de *Discover*, fiz uma *query* pesquisando pelo Event ID 3 e o IP de Destino que observei na tabela:
<img width="1383" height="723" alt="image" src="https://github.com/user-attachments/assets/e9635223-acab-463b-93cb-69aa421ef7a8" />

Encontrei nove logs relacionadas, o ideal a fazer com esse resultado seria criar uma "Linha do Tempo" para correlacionar os eventos.

2. Nessas mesmas logs, procurei pelo *ProcessGUID* do evento. Basicamente isso procurar pelo evento que foi gerado pela sessão do PowerShell;
<img width="1208" height="712" alt="image" src="https://github.com/user-attachments/assets/3903de73-3488-4cfa-a9c7-47cb96c1dcd7" />

Pesquisando por esse valor utilizando a Sintaxe KQL, obtive 15 resultados, e alguns deles geraram Alertas que foram configurados por mim no **Dia 22 - Criação de regra de threshold para atividades do Mythic e criação de Tabela detalhada**
<img width="1183" height="670" alt="image" src="https://github.com/user-attachments/assets/d92172c0-c151-4e79-aa51-cd5a02b757a2" />

Além disso, também procurei por logs envolvendo o **Event ID - 29**, esse tipo de evento é gerado quando o Sysmon detecta a criação de um novo arquivo executável.
<img width="1183" height="670" alt="image" src="https://github.com/user-attachments/assets/2dccc889-68a4-43d9-9f9c-6b99d5778466" />

Vale ressaltar que também, uma boa prática é também verificar os campos de **ProcessID** e **ParentProcessID**.

--- 

## Gerando Alertas no osTicket de Forma Automatizada - Atividades relacionadas ao Mythic C2.
1. Vá até a aba "**Rules**" > **Detection Rules (SIEM)**, também localizada em _Security_; selecione a sua regra de *Mythic C2 - Activities*
2. Clique em "**Edit Rule Settings**" > **Actions** > Selecione o webhook; note que o nosso conector criado no **Dia 25 - Integração ELK Stack e osTicket** já está pré-selecionado. A única coisa que precisamos mudar é o campo "Body", que irá conter as informações do ticket:
```
<?xml version="1.0" encoding="UTF-8"?>
<ticket alert="true" autorespond="true" source="API">
    <name>Elasticsearch</name>
    <email>bananaSecurity@gmail.com</email>
    <subject>{{rule.name}}</subject>
    <phone>11 70707-7070</phone>
    <message type="text/plain"><![CDATA[Alert: {{rule.name}}
    
    Link to investigate the Alert:
    {{rule.url}}]]></message>
</ticket>
```

---

## Análise do Ticket:
No **osTicket**, foi gerado o seguinte alerta após execução do payload na máquina:
<img width="793" height="796" alt="image" src="https://github.com/user-attachments/assets/79fe2548-333e-4dcd-9e88-eeae1a66c6ed" />

Em um cenário real, eu poderia muito bem utilizar a URL do corpo do Ticket para analisar o alerta. Essa URL iria me direcionar para a aba de "Alerts", possibilitando assim que eu comece a triagem do Incidente.
<img width="1256" height="722" alt="image" src="https://github.com/user-attachments/assets/985fe03c-7b5c-4b40-93b3-c9230e891a3b" />

---

## 💡 Lições Aprendidas
- Comandos executados diretamente no através da sessão de C2 rodam apenas na memória do computador, evitando criação de processos. Por isso ao analisar logs de atividades suspeitas, é importante analisar a Telemetria de Rede (IP de destino, IP de origem e portas)
- Realizar pesquisar utilizando os campos `ParentProcessGUID` e `ParentProcessID` permite isolar todas as ações geradas a partir do processo pai, nesse caso o Apollo.exe
- Integrar o SIEM diretamente a uma plataforma de ticketing como o osTicker garante um melhor tempo de reação para o time de SOC.


