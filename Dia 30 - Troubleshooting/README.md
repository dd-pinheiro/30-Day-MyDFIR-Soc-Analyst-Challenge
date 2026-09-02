# 🛡️ 30-Day SOC Analyst Challenge - Day 30

---

## 🎯 Objetivo
- Documentar troubleshooting's realizados durante a instalação e configuração da arquitetura do laboratório.

---

## Introdução
Durante a configuração do laboratório, me deparei com problemas relacionados à conexões entre os servidores e agentes, portanto documentei o passo a passo de cada uma das resoluções desses problemas de conexçao.

### Connection Error - Kibana
Após a instalação e configuração do Kibana no **Dia 4 - Configuração Kibana**, não consegui acessar a interface web do Elasticsearch, apresentando sempre erro de conexão ao tentar conectar no Elasticsearch. Verifiquei o grupo de firewall de rede no Vultr, mas não encontrei nada que apontasse para a causa raiz.
A solução final foi habilitar a porta 5601 no firewall da máquina Ubuntu que hospeda o Elastic e o Kibana, essa é a porta utilizada pelo Kibana para comunicação.
```
ufw allow 5601
```

### Problemas para configurar o Fleet Server no Elasticsearch
Caso tenha problemas assim como eu para instalar a Policy de Fleet no servidor da Frota, crie a seguinte regra de firewall para ser aplicada ao servidor do Elastic & Kibana:
<img width="1073" height="73" alt="image" src="https://github.com/user-attachments/assets/5d49c448-d4ba-413e-87ae-4de8706cc525" />

Essa regra permitirá que o servidor da Frota (Fleet Server) se comunique com o servidor do Elastic e Kibana, pois essa regra será aplicada no grupo de firewall de rede. Além disso, no firewall endpoint da máquina Ubuntu, permita conexões com as portas 9200 e 8220.

<img width="486" height="207" alt="image" src="https://github.com/user-attachments/assets/89b159e6-69c6-431e-809b-02c80b7ddd54" />

A porta 9200 é utilizada para que o **Fleet Server** faça a comunicação com o **Elastic**; já a porta 8220 é utilizado pelos Agentes instalados nos endpoints realizarem a comunicação com o Fleet Server.

### Problemas para gerar telemetria do Elastic Agent no Elasticsearch
Caso as logs não estejam chegando ao elasticsearch, pode ser a falta de uma regra de firewall de rede que permita conexão com a porta 9200.
<img width="1054" height="111" alt="image" src="https://github.com/user-attachments/assets/46de93ca-cbc9-4de3-aebb-6b94a0396845" />

Como esse projeto é apenas um laborátorio, não especifiquei um IP de origem; mas vale ressaltar que em ambiente Produtivos é sempre recomendado criar uma regra voltada para IP's específicos.

---

## 💡Lições Aprendidas
- Investigação de erros de conexão endpoint
- Configuração de regras em Firewall Endpoint e Firewall de rede.
