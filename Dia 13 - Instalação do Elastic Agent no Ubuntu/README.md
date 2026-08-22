# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 13


---

## 🎯 Objetivo do Dia
Instalar e configurar o **Elastic Agent** no servidor Ubuntu exposto para internet para integrá-lo via **Fleet Server**, permitindo a coleta centralizada de logs de segurança e eventos do sistema operacional direto para o SIEM.

---

## Atividades Práticas Realizadas
1. **Acesso ao Fleet Management no Kibana:**
   * Navegue até a seção **Fleet** no painel do Kibana para gerenciar agentes de forma centralizada.
   * Crie ou ajuste de uma **Integration Policy** específica para coletar logs do sistema Ubuntu.

2. **Configuração de Coleta de Logs (`auth.log`):**
   * Defina a fonte da onde a Policy irá obter as logs, nesse caso, será apontado para o diretório `/var/log/auth.log`.

3. **Instalando o Elastic Agent no Ubuntu:**
   * Vá até "Add Agent" e obtenha do comando de instalação gerado pelo Fleet Server.
   * Execute o script fornecido pelo Fleet Server para realizar a instalação do Agente
   * Após a instalação, valide se o agente está gerando as logs de tentativas de conexão SSH, vá até a Aba Discover > Filtre pelo campo agent.name e procure pelo Hostname da sua máquina.

---

## Troubleshooting
Caso tenha problemas para validar o agente, reinicie ele na máquina Ubuntu utilizando a seguinte linha de código:
  ```bash
  sudo systemctl status elastic-agent
