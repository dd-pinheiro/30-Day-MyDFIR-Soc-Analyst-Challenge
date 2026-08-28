# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 19

---

## 🎯 Objetivo do Dia
Nessa aula, você irá criar seu diagrama de ataque; simulando assim ataques reais a sua infraestrutura criada.

---

## Diagrama
### Fase 1 a 3
<img width="482" height="493" alt="image" src="https://github.com/user-attachments/assets/b1891a8c-776c-4c2c-aa46-595580fb1b8b" />

1. **Acesso Inicial**: será onde obteremos as credencias utilizando ataque de força bruta
2. **Reconhecimento**: Essa será a fase de reconhecimento, onde procuraremos informações dentro do sistema, utilizando comandos especificos.
3. **Defense Evasion**: Nessa fase, desativaremos qualquer tipo de proteção que possa nos detectar futuramente, com o intuito de que não sejam geradas logs no Elastic enquanto estivermos instalando o Agente do Mythic na máquina.

### Fase 4 a 6
<img width="481" height="672" alt="image" src="https://github.com/user-attachments/assets/12e17791-a715-4095-895e-934f2e49bad2" />

4. **Execução - Baixando Agente**: Essa é a fase onde baixaremos o agente do Mythic utilizando PowerShell IEX
5. **Command & Control**: Nesta fase, criaremos um arquivo chamado *passwords.txt*. Esse arquivo servirá de exemplo, como quando um atacante acha um arquivo importante dentro da máquina alvo.
6. **Exfiltração**: Aqui, baixaremos o arquivo *passwords.txt* para o nosso Command & Control server.

---

## 💡 Lições Aprendidas
- Criação de diagrama de ataque
- Passos realizados dentro de Ataque Cibernético utilizando o framework **MITRE ATT&CK**

