# 🛡️ 30-Day SOC Analyst Challenge - Day 3

## 🎯 Objetivo do Dia
Configuração do ambiente e início da instalação da base do ELK Stack (Elasticsearch).

---

## ☁️ Infraestrutura de Servidor
Utilizei o provedor Vultr para hospedar o SIEM.

* **Distribuição:** Ubuntu 22.04 LTS
* **Especificações:** 8GB RAM / 2 vCPUs
* **VPC**: Habilitei a configuração de Rede Privada na nuvem para esse servidor, visto que ele será acessado apenas por mim.
* **Configurações Iniciais:**
    1. Acesso via SSH com senha
    2. Atualização do sistema: `sudo apt update && sudo apt upgrade -y`
    3. Foi necessário colocar um grupo de firewall nessa máquina, para bloquear conexões SSH externas, com exceção apenas de meu IP público.
    4. Configuração de Firewall (UFW): habilitar porta 9200 e 5601 (portas utilizadas pelo Elasticsearch e Kibana)

---

## ⚙️ Instalação do Elasticsearch
O Elasticsearch é a espinha dorsal do SIEM, ou seja, aprendendo Elasticsearch você terá uma introdução de como funciona SIEM's empresariais utilizados no mercado hoje em dia.

### Passos realizados:
1. Atualizei o sistema com `sudo apt update && sudo apt upgrade -y`
2. Baixei o elastic search utlizando o comando `wget`. Como a arquitetura do meu servidor é x86, foi necessário especificar isso antes de obter o link para download.
3. Utilizei o comando `dpkg -i` para realizar a instalação manual. Vale ressaltar que a saída desse comando deve ser salva em seu bloco de notas, visto que nessa saída tem a senha de superuser do usuário do Elastic, utilizaremos essa senha nas próximas aulas para logar no Kibana.

### Configurações de Segurança (Resumo):
* Editei o arquivo `/etc/elasticsearch/elasticsearch.yml`, descomentei e alterei as seguintes linhas:
    * `network.host: 45.76.255.250` (Em meu caso, esse é o IP público da Instância).
    * `http.port: 9200` Mantive a porta padrão do elastic search.
* Ativação e inicialização do serviço:
  ```bash
  sudo systemctl daemon-reload
  sudo systemctl enable elasticsearch
  sudo systemctl start elasticsearch

### Configuração de Firewall
Para evitar ataques de Brute Force SSH neste servidor, criei a seguinte regra de Firewall no Vultr:
![regrafirewall](https://github.com/dd-pinheiro/30-Day-MyDFIR-Soc-Analyst-Challenge/blob/29105d4813a96242e8921b618d4902e1430e9b6e/Dia%203%20-%20Configura%C3%A7%C3%A3o%20Elasticsearch/regrafirewall.png)

---

## 💡 Lições Aprendidas e Desafios
- Criação de regras de firewall endpoint e firewall de rede
- Configuração inicial do Elastic


