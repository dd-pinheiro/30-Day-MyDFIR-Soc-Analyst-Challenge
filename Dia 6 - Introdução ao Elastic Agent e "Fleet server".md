# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 6

## 🎯 Objetivos de Aprendizagem
* Compreender o papel dos **Beats** (Filebeat, Winlogbeat, etc.).
* Entender o funcionamento do **Elastic Agent** e do **Fleet Server** para o gerenciamento centralizado.
* Mapear como a telemetria flui dos endpoints (servidores/estações) até o servidor Elasticsearch/Kibana.

---

## Conceitos Chave Explorados

1. **Beats vs. Elastic Agent:**
   * **Beats:** Coletores de telemetria focados em propósitos específicos (ex: *Winlogbeat* para logs de eventos do Windows, *Filebeat* para arquivos de texto/logs).
   * **Elastic Agent:** Um único agente que gerencia múltiplas integrações (segurança, métricas, logs) e é controlado de forma centralizada através de um Fleet Server (Servidor da frota)

2. **Fleet Server:**
   * Um **Fleet Server** ou Servidor da Frota em português, é um componente que conecta diversos agentes a uma "Frota". Ele suporta diversas conexões de Agentes, seja Elastic Agents ou *Beats*;
   * Permite atualizar políticas de segurança, adicionar novas integrações de logs e gerenciar dezenas de endpoints diretamente pela interface do Kibana sem precisar acessar cada máquina individualmente.

---

## 💡 Lições Aprendidas e Desafios
- Qual a diferença entre *Beats* e *Elastic Agente*
- O que é um Fleet Server e qual o propósito dele em uma infrastrutura
