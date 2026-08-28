# 🛡️ 30-Day SOC Analyst Challenge - Day 5

## 🎯 Objetivo do Dia
Configuração e provisionamento do ambiente de endpoint (**Windows Server 2022**) na nuvem, preparando o terreno para a futura geração de telemetria e coleta de logs que serão enviadas para o nosso SIEM.

---

## Arquitetura e Decisões de Infraestrutura
Para simular um ambiente corporativo real e coletar dados de ataques posteriormente, adicionei uma máquina virtual Windows Server em nosso ambiente:
* **Sistema Operacional:** Windows Server 2022
* **Especificações**: 1GB RAM - 1vCPU
* **Provedora de Nuvem:** Vultr
* **Posicionamento de Rede:** A instância foi colocada em uma subnet/região dedicada, separada conceitualmente do servidor do SIEM (Não está na mesma Rede Local da nuvem), permitindo simular tráfego externo e rotas de ataque de forma clara.

