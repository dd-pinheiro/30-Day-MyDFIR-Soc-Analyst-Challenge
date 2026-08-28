# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 13


---

## 🎯 Objetivo do Dia
Instalar e configurar o **Elastic Agent** no servidor Ubuntu exposto para internet para integrá-lo via **Fleet Server**, permitindo a coleta centralizada de logs de segurança e eventos do sistema operacional direto para o SIEM.

---

## Atividades Práticas Realizadas
1. **Acesso ao Fleet Management no Kibana:**
   * Navegue até a seção **Fleet** no painel do Kibana para gerenciar agentes de forma centralizada.
   * Crie ou ajuste de uma **Integration Policy** específica para coletar logs do sistema Ubuntu.
   * Defina a fonte da onde a Policy irá obter as logs, nesse caso, será apontado para o diretório `/var/log/auth.log`.
Deixei bem resumido esse passo a passo, porque é bem parecido com a configuração de Política e Configuração de Agente feita no **Dia 7 - Configuração do Elastic Agent e Fleet Server**; a única mudança vidente é que a na hora de criar a *Policy* do Linux, foi utilizada a integração `system-4`.
<img width="1157" height="66" alt="image" src="https://github.com/user-attachments/assets/548adc0a-70d6-4e5d-a3d5-8f43b3c46d78" />


2. **Instalando o Elastic Agent no Ubuntu:**
   * Vá até "Add Agent" e obtenha do comando de instalação gerado pelo Fleet Server.
   * Execute o script fornecido pelo Fleet Server para realizar a instalação do Agente. Verifique se o Agente foi configurado da forma correta na janela inicial:
<img width="1221" height="434" alt="image" src="https://github.com/user-attachments/assets/db8268d6-7e5b-47f6-9a02-dba09f23052b" />

   * Após a instalação, valide se o agente está gerando as logs de tentativas de conexão SSH, vá até a Aba Discover > Filtre pelo campo agent.name e procure pelo Hostname da sua máquina.
<img width="1238" height="626" alt="image" src="https://github.com/user-attachments/assets/79ec41f0-2146-45d4-b999-83eb58bef1b4" />

---

## Troubleshooting
Caso tenha problemas para validar o agente, reinicie ele na máquina Ubuntu utilizando a seguinte linha de código:
  ```bash
  sudo systemctl restart elastic-agent
```
---

## 💡 Lições Aprendidas e Desafios
- Criação e Integração de politica para hosts Linux/Unix
- Instalação de Elastic Agent em uma máquina Linux
