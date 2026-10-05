# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 15

---

## 🎯 Objetivo do Dia
Compreender os conceitos fundamentais do **Remote Desktop Protocol (RDP)**; analisando como esse serviço é frequentemente utilizado por atacantes em incidentes de ransomware e explorando técnicas de avaliação de exposição e segurança para acessos remotos.

---

## 🔗 RDP - Remote Desktop Protocol
Esse protocolo é utilizado para uma comunicação entre um Servidor e um Cliente. O RDP é encapsulado e utiliza criptografia com o protocolo TCP da camada de Transporte do modelo TCP/IP; utiliza a porta 3389 por padrão.

### Por que é utilizado?
Como já dito anteriormente, é utilizado para acesso remoto. Assim, disponibiliza acessibilidade e conforto para realizar troubleshooting em um computador que está a quilômetros de distância. No entanto, a utilização desse protocolo apresenta algumas desvantagens, por exemplo, o RDP é explorado em 90% dos ataques cibernéticos.

### Como os "Hackers" exploram o RDP?
Uma das principais maneiras que eles exploram esse protocolo é adquirindo acesso à rede de uma organização através de um dispositivo com RDP exposto para a internet, seja utilizando ataques de força bruta, credenciais fracas ou até credenciais vazadas em ataques anteriores.
Os atacantes utilizam serviços OSINT como **shodan.io** ou **censys.com** para encontrar dispositivos com RDP exposto para a internet.

---

## 🛡️Melhores Práticas e Mitigações de Segurança
Para proteger ambientes corporativos contra o abuso de RDP, são recomendadas boas práticas:

* **Uso de VPN Corporativa:** Restringir o acesso ao RDP por meio de uma rede virtual privada segura, evitando a exposição direta da porta `3389` para a internet.
* **Autenticação Multifator (MFA):** Obrigar o uso de MFA para qualquer tentativa de conexão remota.
* **hardening de Contas:** Eliminar contas padrão ou genéricas e aplicar políticas rígidas de expiração e complexidade de senhas, em conjunto com camadas de Multifator de autenticação.

--- 

## 💡 Lições Aprendidas
- O que é **Remote Desktop Protocol RDP** e para que é utilizado
- Como os atacantes exploram esse protocolo para ataque
- Práticas de mitigação

