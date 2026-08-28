# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 10

---

## 🎯 Objetivos de Aprendizagem
* Compreender como o Elastic Agent coleta as logs
* Atualizar e aplicar políticas de integração (*Agent Policies*) no painel do Fleet para incluir no monitoramento do Sysmon.
* Validar no Kibana se os eventos gerados pelo Sysmon estão chegando corretamente ao SIEM.

---

## Passo a passo a configuração:
### 1) Adicionando Integração do Sysmon
1. No homepage do Elastic, clique em "**Add Integrations**", logo em seguida, procure por *Custom Windows Event Logs*
2. Preencha os campos **Integration Name** e **Description**. O campo "Channel Name" deve conter o nome do completo do Sysmon, para obter essa informação siga o passo a passo abaixo no Event Viewer do Windows:
<img width="1323" height="792" alt="image" src="https://github.com/user-attachments/assets/de6ba3e1-a2fd-4402-b2cf-df8fbbc8667d" />
<img width="1380" height="831" alt="image" src="https://github.com/user-attachments/assets/1e16d78a-fc49-4536-abe9-713ab4ab46fd" />
3. Clique em "Next"; Adicione essa integração na politica recém criada no Dia 9, que no meu caso a nomeei de Windows Policy.
<img width="753" height="251" alt="image" src="https://github.com/user-attachments/assets/4b250434-11f4-45db-8465-ea231ea3190d" />

4. Por fim, clique em "**Save and Deploy Changes**".


### 2) Adicionando integração do Windows Defender
1. Realize o mesmo processo feito em **Adicionando Integração do Sysmon**, porém customize a integração do Windows Defender para apenas capturar logs relacionadas aos *Event ID's 1116,1117* e *5001*
2. Por fim, selecione a política recém criada do Windows, e clique em "**Save and Deploy Changes**"

### 3) Verificação das Logs
Ao realizar o Passo 1 e 2, verifique se as logs já estão sendo geradas na aba "Discover" no Elasticsearch.

---

## Dicas e Resolução de Problemas
* **Atraso na Ingestão (Delay):** Se os logs não aparecerem imediatamente, verifique o status do Elastic Agent na máquina local (serviço rodando) e confira se há algum erro de permissão de leitura nos canais de eventos do Windows.


---

## 💡 Lições Aprendidas e Desafios
- Adicionando integração do Sysmon e Windows Defender no Fleet Server
- Gerenciamento de políticas
