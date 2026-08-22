# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 11

---

## 🎯 Objetivo do Dia
Compreender o conceito de **ataques de força bruta (Brute Force Attacks)**, explorar suas variações mais comuns e conhecer algumas das ferramentas mais utilizadas 

---

## O que é um Ataque de Força Bruta?
Um ataque de força bruta (Brute-Force Attack) é um tipo de ataque onde o adversário usa todo tipo de combinação de senha com o intuito de comprometer a conta de um usuário. Existem variações deste ataque, no entanto entraremos em detalhes de apenas três delas.

### Brute Force Attack
Esse ataque utiliza um método "Try and Error" na tentativa de comprometer a conta de um usuário

### *Dictionary Attack*
Similar ao ataque de força bruta, no entanto utiliza uma "word list" que contém palavras comuns, frases e senhas achadas em vazamento de dados.

### *Credential Stuffing*
Isso é onde o atacante obtém uma lista de vazamento de dados e tenta todo tipo de combinação de usuário e senha.

---

##  Ferramentas Ofensivas Comuns
Existem diversos tipos de ferramentas para realizar ataques de força bruta, abaixo citaremos três das mais utilizadas:

| Ferramenta | Descrição / Função Principal |
| :--- | :--- |
| **Hydra** | Ferramenta rápida e versátil para quebra de senhas via rede, suportando múltiplos protocolos (SSH, FTP, RDP, HTTP, etc.). |
| **Hashcat** | Uma das ferramentas de recuperação de hash e senhas mais rápidas e avançadas do mercado. |
| **John the Ripper** | Muito utilizado no pentesting empresarial e quebra de senhas offline |

---

## 🛡️ Perspectiva do SOC: Detecção e Mitigação
O papel fundamental de um analista SOC envolve mitigar e criar barreiras contra essas ameaças. As principais estratégias incluem:
* **Implementação de MFA (Autenticação Multifator):** A defesa mais crítica; mesmo que o atacante descubra a senha por força bruta, ele será bloqueado pelo segundo fator de autenticação.
* **Bloqueio de Contas e Rate Limiting:** Configurar políticas de bloqueio temporário após um número X de falhas consecutivas de login para desacelerar ou impedir os ataques.
* **Políticas de Senhas Fortes:** Incentivar senhas longas (*passphrases*) e complexas envolvendo caracteres especiais, letras maiúsculas e números.
* **Monitoramento de Logs e Alertas:** Investigar logs de falhas de autenticação (`Failed Login`) em sistemas críticos (como eventos do Windows Security ID 4625 ou logs de acesso SSH em servidores Linux).

