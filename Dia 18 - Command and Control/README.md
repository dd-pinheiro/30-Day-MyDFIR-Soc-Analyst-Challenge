# 🛡️ MyDFIR: 30-Day SOC Analyst Challenge - Day 18

---

## 🎯 Objetivo do Dia
Nessa aula, você irá aprender o que é um servidor de *Command and Control*; o porquê ele é importante; quais são as ferramentas/frameworks; e como o Mythic C2 Framework funciona.

---

## Apresentação 
### O que é Command & Control?
Um servidor de Command & Control é um servidor o qual o atacante utiliza para obter controle do computador da vitima, aumentando assim o vetor de ataque, expondo a vítima a diversos tipos de ataques.

### Porque é importante para o atacante?
É importante, pois com o C2 (sigla para Command & Control) o atacante pode performar:
- Roubo de credenciais
- Movimento lateral na rede
- Exfiltração de dados
- Roubar informações sensíveis
- Executar Ransomware.
Qualquer que seja o objetivo, o atacante deve ter acesso ao ambiente para performar a ação, e a forma mais comum de ter acesso ao ambiente é através de um Canal C2.

---
## Ferramentas/Frameworks comuns utilizados para Command & Control
Existem diversas ferramentas e frameworks usados para Comamnd & Control, mas neste video foi explicado as quatro mais utilizadas no mercado, sendo elas:
### Metasploit
Uma ferramenta open-source amplamente usada em cenários de *pentesting* e exploração de vulnerabilidades. Ela é utilizada para obtenção de informações, verificação de vulnerabilidades, pós exploração e melhoras na defesa.

### Cobalt Strike
Essa é uma ferramenta de uso comercial, desenhada justamente para a simular um ataque, realizar *pentesting* e operações de *Red Teaming*. Essa ferramenta é comumente vista em ambientes comprometidos. A boa noticia disso é que por ser uma ferramenta muito utilizada, agências de Threat Intelligence criaram ferramentas com o intuito de ajudar analistas a detectar o Cobalt Strike. Um recurso que você pode utilizar é o [https://thedfirreport.com/]

### Sliver
Sliver é uma ferramenta open-source para simular ataques. Esse framework é fácil de configurar, o que o torna bem perigoso, pois qualquer um pode utilizá-lo. **Sliver** suporta diversas maneiras de estabelecer uma conexão *Command & Control*, seja utilizando protocolos como MTLS, HTTP, HTTPS, DNS e entre outros. 

### Mythic
Esse será o framework que usaremos para esse desafio. Esse framework foi construído a base de docker, docker compose e a linguagem de programção Golang. Ele utiliza uma interface web para gerenciar sua conexão C2. Ao utilizar **Mythic**, você terá a capacidade de baixar payloads prontos e criar *C2 profiles*.
*C2 Profiles* nada  mais é um perfil criado pelo Mythic que tem o intuito de indicar como um agente deve se comunicar com o servidor do Mythic.

---

## Lições Aprendidas
- O que é Command & Control
- Porque Command & Control é importante para um atacante
- Quais são as ferramentas/frameworks utilizados
