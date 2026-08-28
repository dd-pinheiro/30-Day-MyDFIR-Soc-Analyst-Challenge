# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 9

---

## 🎯 Objetivos de Aprendizagem
* Realizar o download e a extração do Sysmon (parte do pacote Sysinternals).
* Utilizar um arquivo de configuração confiável
* Instalar e validar o serviço do Sysmon em um ambiente Windows.

---

## Passo a Passo para instalação
Os passos citados abaixo, devem ser feitos em sua máquina Windows Server 2022 que foi configurada no **Dia 5** deste desafio.

### 1) **Obtenção das Ferramentas:**
   * Baixe a ferramenta do **Sysmon** diretamente do site oficial da Microsoft (Sysinternals).
   * Obtenha um arquivo de configuração confiável; neste caso eu utilizei o arquivo de configuração do olafhartong, disponível no github (https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml)

### 2) **Instalação e Aplicação da Configuração:**
   * Abra o prompt de comando (CMD ou PowerShell) com privilégios administrativos e vá até o diretório onde o Sysmon foi instalado.
   * Execute o binário do sysmon e especifique o arquivo de configuração com o comando abaixo: 
     ```cmd
     sysmon64.exe -i [arquivo de configuração]
     ```

### 3) **Validação do Funcionamento:**
   * Confirme a existênca do serviço Sysmon nos Serviços do Windows (`Services.msc`).
   * Faça a verificação inicial das logs geradas pelo Sysmon no **Event Viewer**, seguindo o caminho: `Applications and Services Logs > Microsoft > Windows > Sysmon > Operational`.

---

## ⚠️ Atenção!
* **Importância de uma boa Configuração (XML):** Instalar o Sysmon sem um arquivo de configuração personalizado (usando apenas as configurações padrão) pode gerar uma quantidade massiva de logs.
* Utilize um arquivo de configuração sysmon confiável.

---

## 💡 Lições Aprendidas e Desafios
- Instalação do Sysmon no Windows
- Importação de um arquivo de configuração para o Sysmon.
