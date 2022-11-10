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

Será entregue um dashboard em PowerBI, para gestão dos indicadores e rotina de atendimento dos processos de triagem do pronto-socorro. Dessa forma, o trabalho de categorização de pacientes na triagem por meio de técnicas de business intelligence e análise e exploração de dados, poderá auxiliar esses profissionais em uma análise mais rápida para ajudar a acelerar o fluxo de atendimento de urgências e emergências.

### Backlog do Produto

![Captura de tela 2022-11-10 163457](https://user-images.githubusercontent.com/96497622/201200410-6dd9b6e8-d167-4f9c-9fc1-15f4ee15424b.png)

## 4. Coleta e Extração dos Dados

O dataset a ser utilizado foi extraído da plataforma de dados abertos [Kaggle](https://www.kaggle.com/datasets/ilkeryildiz/emergency-service-triage-application) e possui 1267 registros de pacientes admitidos em um pronto-socorro da Coreia do Sul entre os meses de outubro de 2016 e setembro de 2017.

| Atributo | Tipo | Descrição |
|--- |--- |--- |
| id_paciente | int | Chave primária ID do paciente
| genero | varchar(10) | 1: Feminino, 2: Masculino
| idade | int | Idade (anos)
| id_transporte | int | 1: A pé, 2: Ambulância pública, 3: Veículo próprio, 4: Ambulância privada, 5: Veículo público, 6: Cadeira de rodas, 7: Outro
| ferimento | int | 1: Sem ferimento, 2: Com ferimento
| queixa_paciente | varchar(45) | Descrição da queixa do paciente
| id_estado_mental | int | 1: Consciente, 2: Resposta verbal, 3: Resposta a dor, 4: Incosciente
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

## 5. Ferramentas

## 6. Técnicas de Análise

## 7. Resultados
