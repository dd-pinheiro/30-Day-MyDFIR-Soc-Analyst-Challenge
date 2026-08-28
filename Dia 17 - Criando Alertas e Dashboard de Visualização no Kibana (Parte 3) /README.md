# 🛡️ MyDFIR SOC Analyst Challenge - Dia 17: Criação de Dashboards e Monitoramento de RDP/SSH

---

## 🎯 Objetivo do Dia
Neste dia, você aprenderá a criar um Dashboard que mostrará as atividades RDP no ambiente.

---


## Atividades Práticas realizadas
### 1) Criação de Dashboard para atividades RDP
Da mesma forma que foi criado um Mapa no **Dia 14** para eventos relacionados ao SSH, você criará outro Mapa; porém neste mapa deve detalhar apenas atividades RDP (Falhas e Autenticações bem sucedidas).
1. Vá até a aba "Maps" > pesquise pela *Query* `event.code: 4625 and agent.name: BobServer` > Add Layer > Selecione o modelo *Choropleth* e adicione em um dashboard existente.
2. Faça o mesmo processo que no mapa acima, porém que a *Query* pela seguinte: `event.code: 4624 and (winlog.event_data.LogonType: 10 or winlog.event_data.LogonType: 7)`
3. Recomendo que deixe os dois mapas lado a lado para uma melhor comparação:
<img width="1430" height="347" alt="image" src="https://github.com/user-attachments/assets/5252dc5e-2dbe-4b33-84e0-55311f93b153" />

### 2. Integração com Mapas Geográficos e Tabelas Detalhadas
Nesta parte, logo abaixo de cada um desses Mapas, foi criada uma tabela para obter uma visualização mais detalhada de cada atividade envolvendo os protocolos SSH e RDP.
1. Em seu dashboard, vá até "**New**" > "**Visualization**"
2. Nessa tela, faça a pesquisa da sua query, seja SSH ou RDP
3. Agora, arraste os campos localizados no canto direito da tela para o centro. Minha recomendação é utilizar os seguintes campos: `timestamp source.ip user.name source.geo.contry_name`.
<img width="1429" height="766" alt="image" src="https://github.com/user-attachments/assets/50b7fe64-2f8d-46e8-87b1-f319cf809d96" />

4. Por fim, faça os ajustes necessários e clique em "Save and return" para sair da aba de Visualização. Posicione a Tabela embaixo ou ao lado do Mapa respectivo àquela tabela.
---

## 📊 Evidências e Capturas de Tela
### Visualização Mapa e Tabela - Atividades SSH
<img width="1431" height="629" alt="image" src="https://github.com/user-attachments/assets/5bebaedf-14d2-49d1-95e5-813856747532" />

### Visualização Mapa e Tabela - Atividades RDP
<img width="1423" height="674" alt="image" src="https://github.com/user-attachments/assets/fddf19e9-d613-4434-a69e-c77633fabc7e" />

---

## 💡 Lições Aprendidas
- Criação de regras threshold para atividades RDP no Kibana
- Como criar Tabelas de visualização e personalizá-las de acordo com a sua necessidade




