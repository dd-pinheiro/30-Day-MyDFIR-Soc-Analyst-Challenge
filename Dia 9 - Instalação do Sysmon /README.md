# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 9

---

## 🎯 Objetivos de Aprendizagem
* Realizar o download e a extração do Sysmon (parte do pacote Sysinternals).
* Utilizar um arquivo de configuração confiável
* Instalar e validar o serviço do Sysmon em um ambiente Windows.

---

## Passo a Passo para instalação
Os passos citados abaixo, foram feitos na máquina Windows Server 2022 que foi configurada no **Dia 5** deste desafio.

### 1) **Obtenção das Ferramentas:**
   * Baixei a ferramenta do **Sysmon** diretamente do site oficial da Microsoft (Sysinternals).
   * Obtenha um arquivo de configuração confiável; neste caso eu utilizei o arquivo de configuração do olafhartong, disponível no github (https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml)

### 2) **Instalação e Aplicação da Configuração:**
   * No prompt de comando (CMD ou PowerShell) com privilégios administrativos, naveguei até o diretório onde o Sysmon foi instalado.
   * Executei o binário do sysmon e especifiquei o arquivo de configuração com o comando abaixo: 
     ```cmd
     sysmon64.exe -i [arquivo de configuração]
     ```

### 3) **Validação do Funcionamento:**
   * Confirmei a existênca do serviço Sysmon nos Serviços do Windows (`Services.msc`).
   * Fiz a verificação inicial das logs geradas pelo Sysmon no **Event Viewer**, seguindo o caminho: `Applications and Services Logs > Microsoft > Windows > Sysmon > Operational`.

---

## ⚠️ Atenção!
* **Importância de uma boa Configuração (XML):** Instalar o Sysmon sem um arquivo de configuração personalizado (usando apenas as configurações padrão) pode gerar uma quantidade massiva de logs.

---

## 💡 Lições Aprendidas e Desafios
- Instalação do Sysmon no Windows
- Importação de um arquivo de configuração para o Sysmon.
