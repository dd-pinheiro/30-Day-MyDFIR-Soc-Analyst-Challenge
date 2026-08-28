# 🛡️ 30-Day SOC Analyst Challenge - Day 25

---

## 🎯 Objetivo do Dia
o objetivo principal nesse dia automatizar a criação de tickets de incidentes integrando o Elastic SIEM ao osTicket.

---

## 📝 Passo a Passo realizado
### 1) Criação de uma Chave API
1. Vá até ao painel de administrador do **osTicket** > **Manage** > **Select API** > **Add New API Key**:
2. Preencha de acordo com as informações abaixo:
<img width="897" height="654" alt="image" src="https://github.com/user-attachments/assets/840645a2-a64e-4fb4-87e3-eeb643163c8d" />

Vale ressaltar que no campo de endereço de IP, coloque o Endereço de IP privado do servidor que hospeda o **Elastic & Kibana**, pois tanto o servidor do osTicket quanto o servidor Elastic&Kibana devem estar na mesma rede privada na nuvem.

3. Finalize clicando em "Add Key"; aqui você receberá uma chave que será utilizada para integrar o osTicket ao Elastic SIEM.
<img width="868" height="342" alt="image" src="https://github.com/user-attachments/assets/2bf98c8d-422a-4fc0-b261-70eae2161b5a" />

### 2) Configurando a Chave API no Elastic SIEM
1. Na interface gŕafica do Kibana, vá até a aba **Managament** > **Stack Management**
2. Procure pela opção **Connectors** localizada no canto esquerdo da tela; prossiga clicando em "**Create Connector**".
3. Pesquise por "Webhook" e selecione esse conector.
<img width="1242" height="676" alt="image" src="https://github.com/user-attachments/assets/3ce1344b-bced-4bc0-9711-b25cabc2979d" />

4. Preencha os campos **Connector Name**, **Connector settings** e **Authentication** da seguinte forma:
<img width="721" height="669" alt="image" src="https://github.com/user-attachments/assets/57ceff30-9b75-4d85-a6a5-8b906e968a95" />

Agora, selecione "Save & Test"

5. Na janela de "Create an Action", preencha o campo *Body* com o payload XML disponibilizado no Github do osTicket [https://github.com/osTicket/osTicket/blob/develop/setup/doc/api/tickets.md]. Após preencher com o XML, clique em "Run" para realizar o teste.
<img width="706" height="503" alt="image" src="https://github.com/user-attachments/assets/82610f37-69c5-4436-a9a2-810f55dc265b" />

Caso o teste tenha sido realizado com sucesso, feche clicando em "Close", e vá até o painel do osTicket; aqui você deve encontrar dois ticket gerados pelo própria integração do ELK Stack e osTicket utilizando webhooks:
<img width="876" height="391" alt="image" src="https://github.com/user-attachments/assets/fbe23e35-4caf-4c7c-8b41-d5b83f9a09fe" />


--- 

## 💡 Lições Aprendidas & Desafios
- Criação de uma chave API para comunicação entre o ELK Stack e osTicket utilizando Webhooks
- Caso tenha problemas para realizar o teste de conexão, verifique as opções de conectividade entre o servidor do osTicket e Elastic&Kibana, realizando testes de ping.
  
