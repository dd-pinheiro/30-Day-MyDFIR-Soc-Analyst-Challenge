# 🛡️ 30-Day SOC Analyst Challenge - Day 12

## 🎯 Objetivo do Dia
No dia de hoje, será feita a criação de nosso servidor Ubuntu com SSH exposto para internet, que servira como honeypot para gerarmos logs no Elasticsearch

---

## ☁️ Infraestrutura de Servidor
Utilizei o provedor Vultr para hospedar o SIEM.

* **Distribuição:** Ubuntu 24.04 LTS
* **Especificações:** 1GB RAM / 1 vCPUs
* **VPC**: Não se aplica
* **Configurações Iniciais:**
    Não se Aplica

---

## Atividades Práticas Realizadas:

1. **Observação de Tráfego Real (Exposição a Bots):**
   * Ao expor a porta SSH diretamente na internet, a máquina se torna um alvo instantâneo para bots automatizados que buscam por portas administrativas abertas globalmente.
   * Monitoramento dos logs que evidenciam um volume expressivo de tentativas de login automatizadas contra contas padrão (`root`, `admin`, `ubuntu`, etc.).

2. **Análise de Logs de Autenticação (Linux):**
   * Em sistemas baseado em Debian, as logs de autenticação ficam no diretório `/var/log/auth.log` ou podemos obter elas via `journalctl` para rastrear as tentativas de invasão.
   * Mapeamento de endereços IP de origem, frequência das requisições e nomes de usuários mais visados.
   * Para visualizar as logs do arquivo `auth.log` em tempo real, utilize o comando `sudo tail -f /var/log/auth.log`

