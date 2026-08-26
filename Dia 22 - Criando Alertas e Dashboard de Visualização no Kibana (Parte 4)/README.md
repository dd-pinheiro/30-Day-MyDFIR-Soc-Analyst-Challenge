# 🛡️ 30-Day SOC Analyst Challenge - Day 22

--- 

## 🎯 Objetivos
* Criar um threshold de alerta relacionado às atividades que estão sendo geradas pelo nosso Agente do Mythic em nosso Servidor Windows.
* Desenvolver um dashboard Operacional no Kibana para visualizar melhor as atividades suspeitas em tempo real do Windows Server.

---

## 📝 Passo a Passo realizado
### 1) Identificando a *Query* ideal
Da mesma forma que foi feito nos dias anteriores, realizei uma pesquisa utilizando a linguagem KQL.
1. Na pesquisa, filtrei pelo `event.code 1`, que o event ID de *Process Create*; basicamente é o event id sempre que o Windows inicia um novo processo
2. De forma análoga, também inseri na pesquisa o campo `winlog.event_data.Hashes: [número da hash SHA256]`, esse campo vai me ajudar a visualizar a hash especifica colocada como valor; o intuito disso é identificar o malware apenas pela hash, filtrando apenas os eventos que atendem a essa condição
3. Mesmo alterando o nome do nosso payload, o campo `winlog.event_data.OriginalFileName` continuou com o nome original do arquivo, que nesse caso é o nome do Agente o qual estamos utilizando (**Apollo.exe**); a query completa ficou da seguinte forma:
```
event.code: 1 and (winlog.event_data.Hashes: *43CAD499660E87AC660BE78BF4069944D303A57C1FE0BECDFFD29A2277A030A7* or winlog.event_data.OriginalFileName: Apollo.exe)
```
5. Por fim, salvei a query para utilizá-la no próximo passo.

### 2) Criando regra de Threshold
Nesta parte, criei uma regra de detecção baseada na *Query* que salvei anteriormente.
1. No kibana, fui até a aba de **Security** > **Rules** e **Detection rules (SIEM)**. além das duas regras criadas anteriormente (Falhas de login SSH e RDP), criei uma regra baseada nas atividades do Mythic C2.
2. Em "New Rule", coloquei a *query* para as atividades do Mythic e em **Required Fields** inseri os seguintes campos:
<img width="849" height="747" alt="image" src="https://github.com/user-attachments/assets/ae1e35e5-c068-4cdf-8bdb-ffd82ae9301c" />

3. Em "**About Rule**, nomeei de uma forma para que fique possível identificar do que essa regra se trata apenas olhando para o título. Além disso alterei a severidade para Critical.
4. Na tela de "**Schedule rule**" mantive em 5 minutos cada campo. Por fim, ignorei a fase actions e salvei e criei a nova regra.
<img width="1249" height="651" alt="image" src="https://github.com/user-attachments/assets/be40e2bd-3ea4-4500-8e7c-8fee1e7cc07a" />

### 3) Criando Dashboards
Aqui, criei dashboards baseados nos **Events ID's**: *3*, *1* e *5001*; são eles:
- **Event ID 3 - Network Connections (External)**: Qualquer processe que inicie uma conexão remota.
- **Event ID 1 - Process Create**: Qualquer criação de processo, no entanto adaptei-a especificamente para processos que foram criados utilizando o *powershell, cmd* ou *rundll32*.
- **Event ID 5001**: Qualquer atividade relacionado ao Windows Defender que informa que ele foi desativado.
Não entrarei em tantos detalhes de como fiz acrescentei as Tabelas Detalhadas, porque isso já foi feito no **Dia 17 - Criação de Dashboards e Monitoramento de RDP/SSH**, contudo, saiba que o resultado final foi esse:
<img width="1440" height="816" alt="image" src="https://github.com/user-attachments/assets/267bc877-0f5a-4d76-b156-ca4ca134e3a9" />

---

## 💡 Lições Aprendidas e Desafios
- Pesquisa detalhada de query utilizando operadores `OR` e `AND`
- Visualização da Query e identificação de hashes de arquivo
- Criação de regras de Threshold e inserção de campos personalizados

