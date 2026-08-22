# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 7

---

## 🎯 Objetivos de Aprendizagem
* Configurar e implantar um Fleet Server conectado diretamente ao Elasticsearch/Kibana.
* Gerar e utilizar *enrollment tokens* para autenticação de agentes com o Fleet Server
* Instalar o Elastic Agent em um ambiente Windows Server.
* Lidar com regras de firewall e troubleshooting de conexões

---

## ☁️ Infraestrutura de Servidor
Foi utilizado o provedor Vultr para hospedar o Fleet Server.

* **Distribuição:** Ubuntu 22.04 LTS
* **Especificações:** 4GB RAM / 1 vCPUs
* **VPC**: Não se aplica
* **Firewall Group**: Adicione a seguinte regra de firewall em seu servidor:

<img width="1064" height="76" alt="image" src="https://github.com/user-attachments/assets/e0e90b29-0ccd-49f4-8195-41ea8a3e8751" />
Essa regra fará com que os servidores do Elastic&Kibana (configurado no dia 3) e osTicket (Servidor de tickets) se comuniquem com o servidor da frota, para que assim seja possível com que o Servidor da Frota se comunique com o Elasticsearch para gerar logs.

---

## Passos a passo

### 1) **Configuração Fleet Server na Interface Web do Elastic Search**
  1. Vá até a sua Interface Web do Elastic Search, procure pela aba "**Management**" e logo em seguida clique em "**Fleet**"
  2. Clique em "**Add Fleet Server**" > **Quick Start**; preencha o os campos Name e URL (`http://[ip público do seu servidor]:[Porta utilizada]`); prossiga clicando em "**Generate Fleet Server Policy**". De forma análoga, siga o exemplo da imagem abaixo:
<img width="1152" height="169" alt="image" src="https://github.com/user-attachments/assets/d7cf26a8-f690-4a39-bd30-7d296bd6dd2d" />
Por fim, realize a conexão SSH em seu servidor Fleet Server, e siga o passo a passo para instalação do Fleet Server. Caso tenha seguido o passo a passo da forma correta, você receberá uma notificação na Interface Web do Elastic informando que o Fleet Server foi conectado.


### 2) **Instalação do Elastic Agent:**
  1. Após a conclusão do **Passo 1**, prossiga clicando em "**Continue enrolling Elastic Agent**" > Insira o nome da sua Politica e clique em "Create Policy"
  2. Selecione o método de instalação do Windows Elastic Agent e siga o passo a passo. Vale ressaltar que o script de instalação deve ser executado no PowerShell como Administrador.

---

## 🔍 Desafios e Troubleshooting (Resolução de Problemas)

Durante a conexão do agente com o servidor Fleet, você irá se deparar com problemas de rede. Os principais pontos de atenção mapeados hoje foram:
* **Portas de Comunicação:** Certificar-se de que as portas essenciais (como a **8220** para o Fleet Server e **443/9200**) estão devidamente abertas.
* **Firewalls e Regras de Subrede:** Validação de regras de firewall tanto no provedor de nuvem (ex: Vultr/Oracle Cloud) quanto nas configurações locais do sistema operacional, é recomendado que habilite as portas **8220,443 e 9200** utilizando `ufw allow` no Ubuntu.

> **Lição Aprendida:** Verifique os padrões de configuração de firewall endpoint (`iptables`/`ufw`) ao diagnosticar falhas de comunicação entre as aplicações.

---
