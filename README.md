# Dashboard para Gestão de Triagem em Prontos-Socorros

<img width="1800" alt="Triagem Hospitalar" src="https://user-images.githubusercontent.com/96497622/201183316-0a61a1a5-a99f-4bdb-9aac-0edd12e43216.png">



## 1. Objetivo

Este projeto foi desenvolvido para fins de conclusão do curso de MBA em Business Intelligence da [XP Educação](https://www.xpeducacao.com.br/). O objetivo é integrar os conhecimentos aprendidos durante os módulos do curso e aplicar em desafio de cenário real, utilizando técnicas e conceitos de design thinking. 

Este repositório é um resumo do relatório final elaborado para o Projeto Aplicado e será apresentado abaixo com o contexto do desafio e as etapas até chegar na solução.



## 2. Contexto

Analisando o contexto das unidades de pronto-socorro de hospitais, notou-se uma forte importância no processo de priorização de atendimentos em níveis de gravidade. Tal decisão impacta significativamente a priorização e agilidade de atuação do tratamento em pacientes com sintomas e casos com risco maior de se tornarem emergências. A classificação existente e amplamente utilizada em boa parte do mundo é a triagem de Manchester, que divide os pacientes em cinco categorias de riscos, com base em cores distintas: Emergência, Muito Urgente, Urgente, Pouco Urgente e Não Urgente.

Os centros de triagem em prontos-socorros geralmente são o gargalo dos atendimentos. É importante aprimorar o processo de triagem desta etapa inicial do atendimento para otimizar a tomada de ação e aumentar o tempo de resposta aos sintomas e efeitos que nem sempre são perceptíveis.

### Matriz CSD &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Observação do tipo POEMS

![eeCaptura de tela 2022-11-10 152629](https://user-images.githubusercontent.com/96497622/201188103-c19f3ed3-33e4-42ff-8b46-044a98b43a4c.png)

### Personas

Foram elaborados os mapas de empatia do paciente e do enfermeiro, nesta ordem.

![Captura de tela 2022-11-10 145743](https://user-images.githubusercontent.com/96497622/201183381-6a790a0d-2723-49d0-b3a4-9c142347d1f6.png)

### Canvas da Proposta de Valor

<img width="1046" alt="Canvas" src="https://user-images.githubusercontent.com/96497622/201183422-c6875563-afe1-40c6-8c84-d9d5369e0454.png">

### Hipóteses &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Priorização de Ideias

![Captura de tela 2022-11-10 152434](https://user-images.githubusercontent.com/96497622/201187854-714118e2-38a0-43e0-a508-6bfb9026857e.png)



## 3. Solução Proposta

Será entregue um dashboard em `Power BI`, para gestão dos indicadores e rotina de atendimento dos processos de triagem do pronto-socorro. Dessa forma, o trabalho de categorização de pacientes na triagem por meio de técnicas de business intelligence e análise e exploração de dados poderá auxiliar esses profissionais em uma análise mais rápida para ajudar a acelerar o fluxo de atendimento de urgências e emergências.

### Backlog do Produto

| Sprint 1 | Sprint 2 | Sprint 3 |
|--- |--- |--- |
| A. Teste e validação da base de dados <br> B. Processo ETL e Construção do data warehouse | A. Protótipo do app de triagem assíncrona <br> B. Teste e validação do app de triagem assíncrona | A. Conexão do banco de dados e ETL <br> B. Construção dos dashboards



## 4. Estrutura dos Dados

O dataset utilizado foi extraído da plataforma de dados abertos [Kaggle](https://www.kaggle.com/datasets/ilkeryildiz/emergency-service-triage-application) e possui 1267 registros de pacientes admitidos em um pronto-socorro da Coreia do Sul entre os meses de outubro de 2016 e setembro de 2017.

| Atributo | Tipo | Descrição |
|--- |--- |--- |
| id_paciente | int | Chave primária ID do paciente
| genero | varchar(10) | 1: Feminino, 2: Masculino
| idade | int | Idade (anos)
| id_transporte | int | 1: A pé, 2: Ambulância pública, 3: Veículo próprio, 4: Ambulância privada, 5: Veículo público, 6: Cadeira de rodas, 7: Outro
| ferimento | int | 1: Sem ferimento, 2: Com ferimento
| queixa_paciente | varchar(45) | Descrição da queixa do paciente
| id_estado_mental | int | 1: Consciente, 2: Resposta verbal, 3: Resposta a dor, 4: Inconsciente
| dor | int | 1: Com dor, 2: Sem dor
| escala_dor | int | Escala de dor 0 a 10
| pressao_sistolica | int | Pressão sistólica (mmHg)
| pressao_diastolica | int | Pressão diastólica (mmHg)
| batimentos_cardiacos | int | Batimentos cardíacos (bpm)
| frequencia_respiratoria | int | Movimentos respiratórios por minuto (mrm)
| temperatura | decimal(2,1) | Temperatura corporal (ºC)
| saturacao_oximetro | int | Saturação de oxigênio (%)
| KTAS_enfermeiro | int | Classificação de risco pelo enfermeiro do primeiro atendimento
| diagnostico | varchar(45) | Diagnóstico inicial da triagem
| id_atendimento | int | 1: Liberado, 2: Admissão enfermaria, 3: Admissão UTI, 4: Autoliberação, 5: Transferência, 6: Morte, 7: Cirurgia
| KTAS_expert | int | Classificação de risco pelo enfermeiro do segundo atendimento
| tempo_PS_min | int | Tempo no pronto-socorro (min)
| duracao_triagem_min | decimal(3,2) | Tempo de duração da triagem (min)

Foram escritas instruções `SQL` para criar uma tabela fato 'triage' no `MySQL`, contendo as informações de atendimento de cada paciente. Também foram criadas e populadas as tabelas dimensão 'risco', 'transporte', 'estado_mental' e 'atendimento'.

Foram realizados procedimentos ETL nos dados, ainda em ambiente do banco de dados, para tratar valores ausentes e outliers. Após o ETL as tabelas foram conectadas ao `Power BI`.

![dsfsdfsd](https://user-images.githubusercontent.com/96497622/201231190-cf87e3a4-5f42-4750-9ce0-c7b06757b920.png)



## 5. Técnicas de Análise

Foram utilizadas técnicas de exploração dos dados (AED) para agregação e sumarização dos registros, para atender o objetivo do projeto, além de conceitos de bancos de dados relacionais e modelagem de dados para fazer o relacionamento entre as tabelas.

![Captura de tela 2022-11-10 195140](https://user-images.githubusercontent.com/96497622/201232131-83201a55-839e-4d1c-b4dd-9ca61c42986e.png)

Como o objetivo da construção dos dashboards é auxiliar no processo de triagem, facilitando as atividades dos enfermeiros e médicos plantonistas, o dashboard foi construído em duas frentes distintas: no formato gerencial, que foi chamado de “Visão Geral” e o formato operacional, que foi intitulado “Detalhamento”. Dessa forma, haverá informações resumidas tanto para o chefe em plantão do pronto-socorro, quanto as informações detalhadas a respeito dos atendimentos e das informações médicas dos pacientes para os enfermeiros e técnicos de saúde.

Os planos de fundo das duas telas do dashboard foram construídas no Figma, um editor online para design de interface.



## 6. Resultados

![Captura de tela 2022-11-11 161843](https://user-images.githubusercontent.com/96497622/201425086-1337122e-db2e-4828-b3a3-5edb73a61214.png)

[Link para acessar o dashboard](https://app.powerbi.com/view?r=eyJrIjoiNmQ2Njc4NDgtMDg3ZS00MDU2LTg0MDEtNjEyYzA0NGU4MDZmIiwidCI6IjhlMjFkN2IyLTg5MDYtNGI5OC1hMjNkLTAzYTM0ZjdkYThiMSJ9)

Os visuais interativos desenvolvidos em Power BI apresentam duas telas distintas. E um ponto interessante é a possibilidade de extrair insights tanto gerenciais, quanto operacionais. O dashboard Visão Geral traz informações amplas sobre os atendimentos do pronto-socorro, como a média total de tempo de triagem e a quantidade de pacientes em cada ala do hospital, durante e após a triagem. Já o dashboard Detalhamento contém informações mais específicas da área médica, como a correlação idade vs oximetria, pressão sistólica vs diastólica, além do grau de risco atribuído pelo enfermeiro da triagem inicial e o enfermeiro expert.

### Insights Obtidos

- A média geral do tempo de triagem está em 5,49min. As categorias de risco maior, Risco 1 e Risco 2, apresentam tempo abaixo da média, respectivamente, em 4,87min e 4,61min.
- A maioria dos pacientes atendidos foram classificados nos riscos 4 e 5, compondo 75% do total de pacientes.
- Quanto à avaliação de risco entre a primeira triagem e a triagem expert, atingiu acurácia de 85%, mediante uma meta de 80%, considerado um indicador positivo, ou seja, quanto maior melhor.
- Observa-se que os pacientes encaminhados para UTI não possuem medição de oximetria durante a triagem.



## 7. Experiências Vivenciadas

- Ao longo de 3 sprints, foram desenvolvidas as atividades planejadas no backlog do produto, resultando em uma aplicação que é capaz de receber os dados de registros médicos de pacientes, armazená-los e processá-los para gerar dashboards em tempo real que auxiliam o processo de triagem de prontos-socorros.
- É essencial conhecer a área de negócios para o qual está desenvolvendo um projeto de BI. Neste caso, ter conhecimento dos valores de referências de atributos médicos ajudou a realizar o processo de análise exploratória dos dados e a plotar os gráficos e o estabelecimento das linhas de especificação.
- Foi necessário criar uma coluna para id_paciente, visto que o dataset não tinha um identificador único para cada registro de paciente.



## 8. Próximos Passos

Foi considerado no projeto o desenvolvimento de uma aplicação em `Power Apps` para a coleta assíncrona de informações médicas dos pacientes, antes que cheguem ao pronto-socorro. O aplicativo foi desenvolvido e testado em seu preenchimento, porém ficará como ações a serem desenvolvidas: 
- Desenvolver os comandos para a exportação do preenchimento para uma tabela e;
- Criar conexão entre o aplicativo diretamente para o dashboard em Power BI.
