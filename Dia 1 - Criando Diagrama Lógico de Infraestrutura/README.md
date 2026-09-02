# 🛡️ 30-Day SOC Analyst Challenge - Day 1

## Apresentação Diagrama de Infraestrustura
Neste primeiro dia, realizei a criação de um diagrama lógico para montar a arquitetura do projeto. Para a criação do diagrama abaixo foi utilizado o **draw.io**:

![diagram](https://github.com/dd-pinheiro/30-Day-MyDFIR-Soc-Analyst-Challenge/blob/175edc198ec0d0ecf332b9682fe64e56e23b4ec7/Dia%201%20-%20Criando%20Diagrama%20L%C3%B3gico%20de%20Infraestrutura/diagrama.png)

Em síntese,esse diagrama é constituido por 6 servidores (todos na nuvem), 2 PCs e a Internet. Abaixo será descrito a função de cada um:
#### Analista SOC - PC
Minha máquina física, em um cenário o qual eu serei o Analista e realizarei a análise dos incidentes.

#### Máquina do Atacante (Kali Linux) e Mythic C2
A máquina do atacante irá que atuar como o ofensor da rede, utilizando um servidor de Command & Control com o Mythic instalado.

#### Servidores
Os dois servidores abaixo estarão na mesma Rede Privada de Nuvem e com Regras de Firewall de Rede configuradas:
* Elastic & Kibana server (Para ingestão de logs)
* osTicket Server (Servidor que hospedará o sistema de tickets)

Os outros três servidores que compõem a infraestrutura. Esses devem ficar fora da Rede Privada da Nuvem, ou seja, expostos para a internet.
* Windows Server com RDP exposto para Internet (Servirá como honeypot para obtermos logs)
* Ubuntu com SSH IP exposto para a Internet (Servirá como honeypot para obtermos logs)
* Fleet Server (Controla os agentes do Elasticsearch instalados nos servidores Windows e Ubuntu)

### Nota 📝
Vale ressaltar que os servidores estão dentro do *Cloud Provider* Vultr, que possibilita a máquinas virtuais utilizando recursos na nuvem.

---

## 💡 Lições Aprendidas e Desafios
- Criação de diagrama de visualização de um infraestrutura.






