# 🛡️ 30-Day SOC Analyst Challenge - Day 4

## 🎯 Objetivo do Dia
Instalação e configuração do **Kibana** no servidor na nuvem, estabelecendo a conexão com o Elasticsearch para habilitar a WebGUI e visualização de dados do SIEM.

---

## O que é o Kibana?
O Kibana é a camada de visualização e interface web do ELK Stack. Como analista de SOC, é nele que passamos a maior parte do tempo investigando incidentes, criando dashboards, construindo regras de detecção e explorando logs através da ferramenta `Discover`.

--

## 📝 Nota:
O mesmo servidor que está hospedando o Elasticsearch, estará hospedando o Kibana também. 

---

## 🛠️ Passo a Passo da Instalação

### 1) Instalação do Pacote
Assim como fiz na instalação do Elasticsearch no servidor, instalei o Kibana utilizando os repositórios oficiais do Kibana no mesmo servidor:
```bash
sudo apt update && sudo apt upgrade
sudo apt install kibana -y
```

### 2) Configuração do Kibana (kibana.yml)
Para permitir o acesso remoto à interface web do Kibana (já que ele roda por padrão apenas em localhost), editei o arquivo de configuração localizado em /etc/kibana/kibana.yml:

    Porta de escuta: server.port: 5601 (porta padrão do Kibana).

    Endereço de rede: server.host: "45.76.255.250" (IP Público do meu servidor Ubuntu).

Após alterar o arquivo e salvá-lo, reiniciei ele utilizando `systemctl restart`.

### 3) Gerando Token de Elasticsearch para o Kibana
Fui até o diretório */usr/share/elasticsearch/bin* e executei o arquivo *elasticsearch-create-enrollment-token* utilizando `./elasticsearch-create-enrollment-token`
Com o Token gerado, fui até o navegador e acessei a URL http://45.76.255.250:5601, na qual minha instância está hospedada. Logo em seguida coloquei o token gerado no campo solicitado; por fim, fui até o diretório **/usr/share/kibana/bin** e executei o binário `./kibana-verification-code` para finalizar a sua configuração.

### 4) API Key Permanente
Utilizei o usuário e a senha de superusuário gerada no **dia 2** do desafio. Para manter as logs em funcionamento sem perder histórico, foi necessário realizar uma configuração de três chaves aleatórias no diretório **/user/share/kibana/bin**
1. Executei o binário `./kibana-encryption-keys generate`
2. Salvei as três chaves criptografadas em um bloco de notas; pois elas serão armazenadas no *keystore* do kibana.
3. No mesmo diretório, executei o binário `./kibana-keystore` para cada chave:
```
   root@vultr:/usr/share/kibana/bin# ./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
   Enter value for xpack.encryptedSavedObjects.encryptionKey: [Hash da chave]
   ****************************************************************  
   root@vultr:/usr/share/kibana/bin# ./kibana-keystore add xpack.reporting.encryptionKey  
    Enter value for xpack.reporting.encryptionKey: [hash da chave]
   ****************************************************************  
    root@vultr:/usr/share/kibana/bin# ./kibana-keystore add xpack.security.encryptionKey  
    Enter value for xpack.security.encryptionKey: [hash da chave]
   ****************************************************************  
```
Para conferir o resultado, vá até a interface Web do Elastic Search > Security > Alerts; caso não tenha nenhum aviso nesta página, a configuração foi feita da forma correta.

---

## 💡 Lições Aprendidas e Desafios
- Configuração do Kibana
- Gerando tokens para armazenar dados
- Alteração no arquivo de configuração do Kibana

