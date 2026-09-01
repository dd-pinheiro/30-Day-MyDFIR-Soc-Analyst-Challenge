# 🛡️ 30-Day SOC Analyst Challenge - Day 29

---

## 🎯 Objetivo
- **Implantação a Integração do **Elastic Defend**:** Adicionar o Elastic Defend à *Agent Policy*
- Instalar/Atualizar o Elastic Agent no Endpoint Windows Server
- **Validar a ingestão de Telemetria EDR**: Verificar a chegada os dados de telemetria no Elasticsearch.
- Simular um alerta e resposta ao alerta fornecido pelo EDR - Elastic Defend.

---

## Passo a Passo realizado
Antes de começar vale ressaltar que uma ferramenta **EDR Endpoint Detection & Response** é um software que monitora de forma contínua dispositivos de usuário final (Servidores, celulares, computadores etc), detectando, investimento e até fornecendo automações para as ameaças que acabam escapando de um Antivírus tradicional.

### 1) Adicionando Integração
1. Na aba de **Management**, vá até "Integrations" e adicione o **Elastic Defend**.
2. Preencha da seguinte forma:
<img width="709" height="675" alt="image" src="https://github.com/user-attachments/assets/a3305d65-4ebd-469c-823b-307049aa267c" />

Em "**Select Configuration Settings** selecionei a opção de "EDR Completa", ou seja, vem com todas as *features* essenciais de uma EDR padrão.
Selecionei essa integração especificamente para o *Agent Policy* de meu Servidor Windows.

### 2) Testando Elastic Defender
Para gerenciar as configurações de sua integração, vá até "**Manage**" na aba de Security.
<img width="1253" height="458" alt="image" src="https://github.com/user-attachments/assets/bcbfbcce-180a-4bd2-afee-cfe0a31db301" />

Para testar de forma definitiva a integração do **Elastic Defend**, tentei executar meu payload novamente; no entanto não obtive êxito pois a EDR entrou em ação e identificou que o arquivo executável se trata de uma espécie de vírus e imediatamente apagou o arquivo do meu servidor.
<img width="1015" height="764" alt="image" src="https://github.com/user-attachments/assets/b6e8ebee-684a-4fe1-9932-7ab8ce5edc30" />

Em adição ao aviso na interface gráfico do servidor, o Elastic Defend também é gerado telemetria, sendo possível visualizá-las na aba de *Discover* do Elasticsearch:
<img width="1234" height="723" alt="image" src="https://github.com/user-attachments/assets/7a06518a-c40b-4e7f-9dca-625a671e4786" />
<img width="734" height="783" alt="image" src="https://github.com/user-attachments/assets/1f2b65c5-6457-487c-b458-38baaa8f72ea" />

Dentre essas informações das logs, há vários outros campos que podem ser investigados, tais como:
- `file.name`
- `file.owner`
- `file.path`
- `hash(MD5 ou SHA256)`
Abaixo, segue uma captura de tela com esses campos demarcados
<img width="708" height="738" alt="image" src="https://github.com/user-attachments/assets/3edda518-96e7-4671-96c8-7c637463c0b3" />

Além da telemetria gerada, com a integração do EDR no Windows Server, também foi criado um alerta relacionado às atividades suspeitas:
<img width="1257" height="582" alt="image" src="https://github.com/user-attachments/assets/f6898499-dad6-43f3-8fc9-821c34a1c65b" />

Por padrão esses alertas já geram informações relevantes para um processo de triagem de incidente, mas outros campos podem ser adicionados para facilitar mais ainda o processo de investigação.
<img width="521" height="748" alt="image" src="https://github.com/user-attachments/assets/9482dad3-7fbc-4b47-becf-c189333b5349" />

### 3) Configurando uma ação de resposta
Aqui, configurei um ação de resposta sempre que for gerado um alerta vindo de origem do Elastic Defender - EDR.
1. Na aba de "**Security**" vá até **Detection Rules (SIEM**) > Selecione o alerta do Elastic Defender > **Edit Rule Settings**.
2. Em "Response Actions", selecione Elastic Defend; aqui é possível selecionar uma ação para quando o alerta for gerado. No meu caso selecione a ação de Isolar o host.
<img width="861" height="504" alt="image" src="https://github.com/user-attachments/assets/9c535f3f-1ad3-47a4-b480-df9d416295a5" />

Em relação à ação que escolhi, basicamente, sempre que for identificado uma atividade suspeita, a máquina será isolada da rede local, evitando assim que a ameaça se propague pela rede.
<img width="885" height="526" alt="image" src="https://github.com/user-attachments/assets/40041380-c746-46b6-99c4-6c91037bbd10" />

---

## 💡 Lições Aprendidas e Desafios
- Com a ajuda do Fleet Server é possível realizara instalação de uma EDR e além disso gerenciá-la facilmente através das Agent Policies criadas
- Combinar Logs do Sysmon/Windows Defender com a telemetria do Elastic Defend, reduzindo ainda mais os pontos cegos
- Ações automatizadas disponibilizadas pela EDR - Elastic Defend.
