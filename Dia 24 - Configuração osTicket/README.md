# 🛡️ 30-Day SOC Analyst Challenge - Day 24

## 🎯 Objetivo do Dia
O objetivo do dia 24 foi realizar a instalação e configuração inicial do **osTicket** em uma máquina virtual Windows. O **osTicket** atuará como uma plataforma de Gerenciamento de Incidentes de Segurança (Ticketing System).
No dia 25, iremos realizar a integração do **osTicket** com o **Elasticsearch**.

---

## ☁️ Infraestrutura de Servidor
Utilizei o provedor Vultr para hospedar o SIEM.

* **Distribuição:** Windows Server Standard 2022
* **Especificações:** 2GB RAM / 1 vCPUs
* **VPC**: Deve estar na mesma Rede Local virtual do servidor que hospeda o **Elastic & Kibana**.
* **Configurações Iniciais:**
    Não se Aplica

---

## 📝 Passo a Passo realizado

### 1) Instalação e Configuração do XAMPP
Utilizei o XAMPP para hospedar um servidor web para o osTicket. 
1. Instalei o XAMPP através de seu site oficial [https://www.apachefriends.org/download.html]
2. Após instalação, fui até o diretório do XAMPP e alterei o arquivo *properties*, mudando apenas o valor da linha "apache_domainname" de localhost para o IP público do meu servidor.
3. A próxima alteração que fiz, foi adicionar uma regra de *Inbound* no Firewall endpoint do Windows, permitindo conexões com a porta 80 e 433 (HTTP e HTTPS).
<img width="1007" height="656" alt="image" src="https://github.com/user-attachments/assets/c0c340c7-b57d-4d4d-9317-373e33d514bf" />

### 2) Configuração via Web
