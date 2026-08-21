# Apresentação Diagrama de Infraestrustura
Nessa primeira aula, foi necessário realizar a criação de um diagrama lógico para entendermos melhor como funcionará o ambiente o qual será práticado o monitoramento. Para a criação do diagrama abaixo foi utilizado o **draw.io**:

![diagram](https://github.com/dd-pinheiro/30-Day-MyDFIR-Soc-Analyst-Challenge/blob/175edc198ec0d0ecf332b9682fe64e56e23b4ec7/Dia%201%20-%20Criando%20Diagrama%20L%C3%B3gico%20de%20Infraestrutura/diagrama.png)

Em síntese,esse diagrama é constituido por 6 servidores, 2 PCs e a Internet. Abaixo será descrito a função de cada um:
### Analista SOC - PC
Será a nossa máquina fisica, que fará o papel de Analista SOC

### Máquina do Atacante (Kali Linux) e Mythic C2
A máquina do atacante irá atuar como o ofensor da rede, utilizando Mythic Framework como servidor de Command & Control.

### Servidores
Os dois servidores abaixo estarão na mesma Rede Privada de Nuvem.
* Elastic & Kibana server (Para ingestão de logs)
* osTicket Server (Servidor que hospeda o sistema de tickets)

Os outros três servidores que compõem a infraestrutura devem ficar fora da Rede Privada da Nuvem, ou seja, expostos para a internet.
* Windows Server com RDP exposto para Internet (Servirá como honeypot para obtermos logs)
* Ubuntu com SSH IP exposto para a Internet (Servirá como honeypot para obtermos logs)
* Fleet Server (Controla os agentes do Elasticsearch instalados nos servidores Windows e Ubuntu

#### Nota 📝
Vale ressaltar que os servidores estão dentro do Provedor Vultr, que nos possibilita de criar máquinas virtuais.






