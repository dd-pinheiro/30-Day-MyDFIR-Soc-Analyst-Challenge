# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 10

---

## 🎯 Objetivos de Aprendizagem
* Compreender como o Elastic Agent coleta as logs
* Atualizar e aplicar políticas de integração (*Agent Policies*) no painel do Fleet para incluir no monitoramento do Sysmon.
* Validar no Kibana se os eventos gerados pelo Sysmon estão chegando corretamente ao SIEM.

---

## 🛠️ Passos Executados no Lab

1. **Ajuste da Política no Fleet Server:**
   * Acesso ao painel do Kibana em **Fleet > Agent Policies**.
   * Edição da política aplicada ao endpoint Windows para adicionar uma nova integração voltada a logs do Windows (*Custom Windows Event Logs* ou a integração padrão de segurança do Windows/Sysmon).

2. **Configuração dos Canais de Log:**
   * Mapeamento do caminho correto do canal do Sysmon no Windows Event Viewer (`Microsoft-Windows-Sysmon/Operational`).
   * Garantia de que a coleta estivesse ativa para capturar os principais Event IDs configurados anteriormente nos dias passados (como criações de processos e conexões de rede).

3. **Validação da Ingestão no Kibana:**
   * Acesso ao aplicativo **Discover** no Kibana.
   * Filtragem por índices do Elastic Agent para verificar se os dados brutos (`event.dataset: "windows.sysmon_operational"` ou similar) já estavam sendo indexados e exibidos na timeline.

---

## 🔍 Dicas e Resolução de Problemas
* **Atraso na Ingestão (Delay):** Se os logs não aparecerem imediatamente, verifique o status do Elastic Agent na máquina local (serviço rodando) e confira se há algum erro de permissão de leitura nos canais de eventos do Windows.
* **Filtros de Índice:** Certifique-se de estar buscando pelo padrão de índice correto (`logs-*`) no Discover para não perder os dados recém-chegados.

---

## ✅ Conquistas do Dia
* [x] Política do Fleet atualizada para monitorar o canal operacional do Sysmon.
* [x] Agente enviando dados do endpoint Windows com sucesso.
* [x] Primeiros logs do Sysmon visualizados e validados dentro do Kibana (Discover).

---

## 💡 Próximos Passos
* Avançar para a criação de painéis (*Dashboards*) ou investigação de alertas baseados nesses novos logs que estão chegando ao SIEM.

---
[⬅️ Voltar para o Índice](../README.md)
