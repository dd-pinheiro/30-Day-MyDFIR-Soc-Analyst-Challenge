# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 13


---

## 🎯 Objetivo do Dia
Instalar e configurar o **Elastic Agent** no servidor Ubuntu exposto para internet para integrá-lo via **Fleet Server**, permitindo a coleta centralizada de logs de segurança e eventos do sistema operacional direto para o SIEM.

---

## Atividades Práticas Realizadas
1. **Acesso ao Fleet Management no Kibana:**
   * Fui até a sessão **Fleet** no painel do Kibana para gerenciar agentes de forma centralizada.
   * Criei uma Policy em **Integration Policy** para especificar a coleta de logs do Ubuntu
   * Apontei a fonte das quais serão coletadas as logs, apontei para o diretório `/var/log/auth.log`.
Deixei bem resumido esse passo a passo, porque é bem parecido com a configuração de Política e Configuração de Agente feita no **Dia 7 - Configuração do Elastic Agent e Fleet Server**; a única mudança vidente é que a na hora de criar a *Policy* do Linux, que foi foi utilizada a integração `system-4`.
<img width="1157" height="66" alt="image" src="https://github.com/user-attachments/assets/548adc0a-70d6-4e5d-a3d5-8f43b3c46d78" />

2. **Instalando o Elastic Agent no Ubuntu:**
   * Em "Add Agent" na aba de Fleet Server, obtive o comando de instalação gerado pelo Fleet Server.
   * Executei o script fornecido pelo Fleet Server para realizar a instalação do Agente. Em seguida, verifique se o Agente foi configurado da forma correta na janela inicial:
<img width="1221" height="434" alt="image" src="https://github.com/user-attachments/assets/db8268d6-7e5b-47f6-9a02-dba09f23052b" />

   * Após a instalação, validei se o agente está gerando as logs de tentativas de conexão SSH, na Aba de Discover; filtrei pelo campo agent.name e procurei pelo Hostname da máquina ubuntu.
<img width="1238" height="626" alt="image" src="https://github.com/user-attachments/assets/79ec41f0-2146-45d4-b999-83eb58bef1b4" />

---

## Troubleshooting
Foi necessário reiniciar o agente antes de obter as logs dele, para isso utilizei a ferramenta `systemctl`, que já é embutida no SO:
```
  sudo systemctl restart elastic-agent
```

---

## 💡 Lições Aprendidas e Desafios
- Criação e Integração de política para hosts Linux/Unix
- Instalação de Elastic Agent em uma máquina Linux
