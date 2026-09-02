# 🛡️ 30-Day SOC Analyst Challenge- Day 20

## 🎯 Objetivo do Dia
Criar nosso servidor que servirá como *Command & Control* e também configurar o Mythic dentro do servidor.

---


## ☁️ Infraestrutura de Servidor
Novamente, vale ressaltar que todos os servidores deste repositório estão sendo criados através do Vultr[https://www.vultr.com/]

* **Distribuição:** Ubuntu 22.04 LTS
* **Especificações:** 4GB RAM / 2 vCPUs
* **VPC**: Criado um novo grupo de firewall, com uma regra de Firewall permitindo conexões em todas as portas TCP vindas apenas de meu IP público. Com isso, será possível acessar a interface gráfica do Mythic sem precisar estar na mesma rede local.

* **Configurações Iniciais:**
    Não se Aplica

---

## 📝 Passo a Passo Realizado
### 1) Configurando o Mythic
Vale ressaltar que essas configurações foram feitas no servidor recém criado.
  1. Antes de começar a instalação, atualizei meus repositórios com `sudo apt update & sudo apt upgrade`
  2. Instalei as ferramentas *Docker Compose* e *make* utilizando a linha de comando `sudo apt install docker-compose make`
  3. Clonei o repositório do Mythic no github utilizando a linha de comando `git clone https://github.com/its-a-feature/mythic`
  4. No diretório do mythic que clonei do github e executei o comando `./install_docker_ubuntu.sh`; de forma resumida, esse script irá realizar a instalação do Mythic em sua máquina
  5. Iniciei o serviço do mythic utilizando `mythic-cli start`

### 2) Configuração de Firewall na nuvem
Após finalizar a instalação do Mythic em meu servidor, criei um novo grupo de Firewall de Rede; neste novo *Firewall Group*, criei a seguinte regra:
<img width="907" height="102" alt="image" src="https://github.com/user-attachments/assets/beaec7c2-e416-48b3-8197-b8eff78bbd8e" />

Vale ressaltar que essa regra permitirá conexões em todas as portas apenas do meu IP público. O motivo pelo qual fiz isso é porque utilizarei o Mythic pelo navegador usando o protocolo HTTP, ou seja, apenas o meu IP público conseguirá interagir com o Mythic por conta desta regra de firewall de rede.

### 3) Utilizando o Mythic
1. Para acessar a interface gráfica do Mythic pelo navegador, utilizei a URL *http://[ip público do servidor do mythic]:7443*.
<img width="785" height="674" alt="image" src="https://github.com/user-attachments/assets/d69b2cc5-b28c-41e7-8b04-881912bf5a99" />

Por padrão o mythic é configurado para se comunicar através da porta 7443, mas você pode alterar isso no arquivo de configuração.

2. As credenciais para autenticar no mythic estão disponíveis arquivo **.env** localizado no diretório do Mythic; as credenciais estão nas linhas **MYTHIC_ADMIN_PASSWORD** e **MYTHIC_ADMIN_USER**. Para obtê-las, digitei a seguinte linha de comando especificando o arquivo **.env**:
```
grep -ie MYTHIC_ADMIN_PASSWORD -e MYTHIC_ADMIN_USER .env
```

---

## 💡 Lições Aprendidas e Desafios
- Aplicação de regras no Firewall na nuvem;
- Troubleshooting realizado para liberar a porta 7443 no firewall local da máquina;
- Configuração e hospedagem inicial do Mythic em um servidor;



   
