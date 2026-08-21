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
    3. Configuração de Firewall (UFW): habilitar porta 9200 e 5601 (portas utilizadas pelo Elasticsearch e Kibana)

---

## ⚙️ Instalação do Elasticsearch
O Elasticsearch é a espinha dorsal do SIEM, ou seja, aprendendo Elasticsearch você terá uma introdução de como funciona SIEM's empresariais.

### Passos realizados:
1. Atualizei o sistema com `sudo apt update && sudo apt upgrade -y`
2. Baixei o elastic search utlizando o comando `wget`. Como a arquitetura do meu servidor é x86, foi necessário especificar isso antes de obter o link para download.
3. Utilizei o comando `dpkg -i` para realizar a instalação manual. Vale ressaltar que a saída desse comando deve ser salva em seu bloco de notas, visto que nessa saída tem a senha de superuser do Elastic.

### Configurações de Segurança (Resumo):
* Editei o arquivo `/etc/elasticsearch/elasticsearch.yml` e descomentei as seguintes linhas:
    * `network.host: 45.76.255.250` (Em meu caso, esse é o IP público da Instância).
    * `http.port: 9200` Mantive a porta padrão do elastic search.
* Ativação e inicialização do serviço:
  ```bash
  sudo systemctl daemon-reload
  sudo systemctl enable elasticsearch
  sudo systemctl start elasticsearch

### Configuração de Firewall
Para evitar ataques de Brute Force neste servidor, criei a seguinte regra de Firewall no Vultr:

