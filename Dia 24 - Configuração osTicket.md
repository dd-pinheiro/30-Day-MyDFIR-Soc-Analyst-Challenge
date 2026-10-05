# 🛡️ 30-Day SOC Analyst Challenge - Day 24

## 🎯 Objetivo do Dia
O objetivo do dia 24 foi realizar a instalação e configuração inicial do **osTicket** em uma máquina virtual Windows. O **osTicket** atuará como uma plataforma de Gerenciamento de Incidentes de Segurança (Ticketing System).
No dia 25, iremos realizar a integração do **osTicket** com o **Elasticsearch**.

---

## ☁️ Infraestrutura de Servidor

* **Distribuição:** Windows Server Standard 2022
* **Especificações:** 2GB RAM / 1 vCPUs
* **VPC**: Deve estar na mesma Rede Local virtual do servidor que hospeda o **Elastic & Kibana**.
* **Configurações Iniciais:**
    - Acesso via RDP com senha
    - Necessário colocar o servidor no mesmo grupo de Firewall do *Vultr*, para somente permitir conexões RDP e HTTP/HTTPS com o meu IP público (*allow list*).

---

## 📝 Passo a Passo realizado

### 1) Instalação e Configuração do XAMPP
Utilizei o XAMPP para hospedar um servidor web para o osTicket. 
1. Instalei o XAMPP através de seu site oficial [https://www.apachefriends.org/download.html]
2. Após instalação, fui até o diretório do XAMPP e alterei o arquivo *properties*, alterando apenas o valor da linha "`apache_domainname`" de localhost para o IP público do meu servidor.
3. A próxima alteração que fiz, foi adicionar uma regra de *Inbound* no Firewall endpoint do Windows, permitindo conexões com a porta 80 e 433 (HTTP e HTTPS).
<img width="1007" height="656" alt="image" src="https://github.com/user-attachments/assets/c0c340c7-b57d-4d4d-9317-373e33d514bf" />

### 2) Configuração via Web
1. Aqui, foi necessário alterar a senha do usuário root e pma no painel **phpmyadmin**.
<img width="1011" height="732" alt="image" src="https://github.com/user-attachments/assets/5dd372d4-2263-4ef7-b141-b71ee67e6f16" />

2. Após realizar a alteração através no painel, alterei o arquivo de configuração **config.inc**, adicionando as informações respectivas às alterações que fiz no painel *phpmyadmin*.
<img width="750" height="510" alt="image" src="https://github.com/user-attachments/assets/3f6b145b-67b0-4eb0-9c60-ddf3ce482334" />

### 3) Criando Database
Antes de hospedar o osTicket, criei um database próprio para suportar o sistema de tickets.
- Dentro do phpmyadmin, realizei a criação de um novo database e selecionei a minha conta "root" para ter acesso total ao novo banco de dados.
<img width="1022" height="553" alt="image" src="https://github.com/user-attachments/assets/3697b5eb-9b5b-4fec-880f-ee95a849ff56" />


### 4) Configuração arquivo *htdocs*
1. No site oficial do osTicket [https://osticket.com/] realizei o download do arquivo disponibilizado na aba **Self-hosted**.
2. Realizei a extração do arquivo baixado e copiei as duas pastas dentro do arquivo, sendo elas as pastas **script** e **upload**.
3. Dentro do diretório raiz do XAMPP (**C:\xamp**), fui até a pasta **htdocs** e criei uma pasta chamada **osTicket**; dentro deste diretório colei as pastas **script** e **upload** posteriormente copiadas.
<img width="1022" height="553" alt="image" src="https://github.com/user-attachments/assets/9b1b48bc-064f-4d5a-9ec9-b2bbb1b0f55b" />

*OBS: O arquivo htdocs guarda todo o conteúdo das páginas web hospedadas no XAMPP*

### 5) Instalação e Configuração - osTicket
Após configurar o conteúdo do osTicket no XAMPP, comecei a instalação do osTicket através do navegador.
1. Na URL [http://45.32.212.6/osticket/upload/setup/] comecei a instalação do osTicket. Note que o domínio é o IP público do servidor onde hospedei o osTicket e o caminho são as pastas localizadas dentro do diretório do osTicket.
<img width="1267" height="857" alt="image" src="https://github.com/user-attachments/assets/ab22b2d8-db69-46a7-b34c-cdd482565a43" />

Vale ressaltar que essa URL pode ser acessada apenas por mim, visto que foi configurada uma regra de firewall para aceitar conexões apenas de meu IP público.
2. Para prosseguir com a instalação tive que ir até a pasta **uploads** dentro de osTicket > **include** e renomear o arquivo *ost.sampleconfig* para *ost-config*.
<img width="1045" height="686" alt="image" src="https://github.com/user-attachments/assets/4fd6d48a-1739-4d53-8ee5-a2580d42162f" />

3. Posteriormente, foi necessário preencher alguns campos de configuração inicial para o osTicket; preenchi de acordo com as minhas demandas, apenas deixei padrão a parte de "Database settings" que preenchi da seguinte forma:
<img width="1020" height="372" alt="image" src="https://github.com/user-attachments/assets/cb9f8ed5-c802-40e6-b447-9a586492fc4a" />

Vale ressaltar que essas informações demarcadas devem estar em sincronia com as informações preenchidas no painel *phpmyadmin*, caso contrário, você não conseguirá realizar a configuração do osTicket.
4. Por fim, foi alterei a permissão do arquivo de configuração e acessei as URL do painel principal do Sistema de Tickets.
<img width="1020" height="372" alt="image" src="https://github.com/user-attachments/assets/33021363-64e2-468d-945f-36fad78f89fd" />

---

## 💡 Lições Aprendidas e Desafios
- Instalação e configuração do XAMPP
- Configuração do painel phpmyadmin via web / mudança nos arquivos de configurações
- Criação do banco de dados
- Criação de regra no Firewall do Windows para conexões de entrada.
