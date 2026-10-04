# 🛡️ MyDFIR 30 Days SOC Analyst Challenge - Day 8

---

## 🎯 Objetivos de Aprendizagem
* Compreender o que é o Sysmon e qual o seu papel fundamental no monitoramento de endpoints.
* Entender a diferença entre os logs padrão do Windows (Security Event Log) e a variedade oferecida pelo Sysmon.
* Familiarizar-se com os principais **Event IDs** do Sysmon utilizados em *threat hunting* e análises forenses.

---

## Conceitos Chave Explorados
### O que é o Sysmon?
   * É um serviço de sistema do Windows e um driver de dispositivo que permanece residente na máquina (faz parte do conjunto de ferramenta sysinternals do Windows), monitorando e registrando a atividade do sistema nas logs de eventos do Windows.
   * Ele oferece informações detalhadas sobre criações de processos, conexões de rede e alterações em arquivos/chaves de registro.

### Por que o Sysmon é crucial para um SOC?
   * Os logs nativos do Windows podem ser genéricos ou carecer de informações cruciais sobre *como* um processo foi executado (ex: linha de comando completa, árvore de processos e hashes).
   * O Sysmon captura dados comportamentais complexos que ajudam a identificar técnicas comuns de ataques cibernéticos.

### Principais Event IDs do Sysmon para Monitorar:
   * **Event ID 1:** Process Creation (Criação de processo com linha de comando e hash).
   * **Event ID 3:** Network Connection (Conexões de rede iniciadas por processos).
   * **Event ID 7:** Image Loaded (DLLs carregadas por processos, útil para detectar *DLL injection*).
   * **Event ID 11:** File Create (Criação de arquivos no disco).
   * **Event ID 22:** DNS Query (Consultas DNS realizadas pelos processos).

---

## ⚠️ Pontos de Atenção
* **Volume de Dados e Ruído:** O Sysmon gera uma quantidade massiva de logs. Sem uma configuração adequada, irá mais prejudicar o ambiente de monitoração do que ajudar.

---

## 💡 Lições Aprendidas
- O que é o Sysmon, e porque ele é essencial para um ambiente de **Security Operations Center (SOC)**
- Principais event ID's de segurança.
