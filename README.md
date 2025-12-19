# MVP de Engenharia de Dados – Pipeline de Dados Climáticos

Este repositório apresenta o desenvolvimento de um MVP para a disciplina de Engenharia de Dados, com foco na construção de um pipeline de dados em nuvem aplicado à análise de dados climáticos da cidade de Aracaju (SE).

O objetivo do MVP é demonstrar, de forma prática e funcional, a implementação de um pipeline capaz de coletar, processar, armazenar e analisar dados meteorológicos históricos, aplicando conceitos fundamentais de engenharia de dados.

# Problema proposto do Projeto

O Instituto Nacional de Meteorologia (INMET) é uma plataforma governamental responsável pela disponibilização de dados meteorológicos oficiais referentes às capitais brasileiras. Contudo, esses dados são disponibilizados de forma fragmentada, distribuídos em múltiplos arquivos e intervalos temporais distintos, o que dificulta sua utilização direta para análises integradas. Adicionalmente, os conjuntos de dados podem apresentar inconsistências estruturais e valores ausentes, evidenciando a necessidade de processos sistemáticos de ingestão, tratamento, padronização e consolidação para garantir a confiabilidade das análises climáticas.

Essas limitações dificultam a identificação eficiente e reprodutível do dia mais chuvoso, do dia mais quente e do dia mais frio dos últimos cinco anos, comprometendo análises acadêmicas e estudos de apoio à tomada de decisão relacionados a riscos climáticos e impactos ambientais.

# Solução proposta:

A implementação de um pipeline de dados estruturado e automatizado, capaz de realizar a ingestão, limpeza, padronização, consolidação e análise dos dados climáticos históricos do INMET, permitirá a construção de uma base confiável e reprodutível, viabilizando a identificação precisa dos eventos climáticos extremos (chuva, calor e frio) ocorridos em Aracaju nos últimos cinco anos.

# Objetivo
Desenvolver um MVP de pipeline de dados em nuvem que consolide e processe dados climáticos históricos da cidade de Aracaju (SE), permitindo a identificação do dia mais chuvoso, do dia mais quente e do dia mais frio dos últimos cinco anos.

## Objetivos Específicos:

- Ingerir dados climáticos históricos a partir da base do INMET;

- Tratar e padronizar os dados, corrigindo inconsistências e valores ausentes;

- Consolidar os dados em uma base histórica única e estruturada;

- Filtrar e analisar os dados referentes aos últimos cinco anos;

- Identificar e validar eventos climáticos extremos no período analisado.

# Descrição dos Dados

Os dados utilizados neste projeto são provenientes do Instituto Nacional de Meteorologia (INMET), obtidos a partir da base de dados históricos meteorológicos, que disponibiliza informações como: 
O conjunto de dados utilizado neste projeto é composto por medições meteorológicas horárias, disponibilizadas pelo Instituto Nacional de Meteorologia (INMET). Cada registro representa uma observação realizada em uma estação meteorológica automática, referente a uma data e hora específicas (UTC).

# Desenvolvimento
 Este MVP foi desenvolvido como parte da disciplina de Engenharia de Dados, com foco na validação de um pipeline mínimo, funcional e escalável. O projeto utiliza dados reais e aplica boas práticas de organização, processamento distribuído e análise de dados em nuvem.

1. Coleta e Ingestão de Dados
   
A primeira etapa consistiu no acesso ao portal de dados históricos do INMET (Instituto Nacional de Meteorologia).

- Fonte dos Dados Portal INMET - Dados Históricos (https://portal.inmet.gov.br/dadoshistoricos) 

- Período 2021 a 2025.

- Processo de Extração: Foram baixados arquivos compactados (.ZIP) contendo aproximadamente 584 arquivos CSV por ano, cada um representando uma estação meteorológica brasileira.

- Tratamento Inicial: Para este MVP, foram selecionados exclusivamente os registros da cidade de Aracaju - SE.

- Tecnologia:  Os dados foram carregados para o ambiente Databricks, onde foram processados utilizando Spark para garantir escalabilidade.

2. Modelagem de Dados
   
Para este projeto, optou-se pela arquitetura de Data Lake com uma abordagem Flat (Tabela Única) por conceito. Essa escolha justifica-se pela natureza dos dados meteorológicos (séries temporais), facilitando o consumo imediato para análises exploratórias e modelos de Machine Learning, evitando joins complexos que poderiam degradar a performance em grandes volumes.
### 3. Catálogo de Dados

#### Variáveis Temporais e Meteorológicas
| Coluna | Descrição | Domínio | Min/Max |
| :--- | :--- | :--- | :--- |
| Data | Data da observação meteorológica | AAAA-MM-DD | 2021 a 2025 |
| Hora UTC | Hora da medição (UTC) | HHMM UTC | 00:00 a 23:00 |
| Precipitação | Volume total acumulado | Real (mm) | 0 a 95.40 mm |

#### Pressão Atmosférica (mB)
| Coluna | Descrição | Min/Max Esperado |
| :--- | :--- | :--- |
| Pressão Estação | Pressão ao nível da estação | 900 a 1100 mB |
| Pressão Máx | Maior valor na hora anterior | 900 a 1100 mB |
| Pressão Mín | Menor valor na hora anterior | 900 a 1100 mB |

#### Temperatura e Ponto de Orvalho (°C)
| Coluna | Descrição | Min/Max Esperado |
| :--- | :--- | :--- |
| Temp. Bulbo Seco | Temperatura atual do ar | 10°C a 45°C |
| Temp. Ponto Orvalho | Saturação de umidade | 5°C a 30°C |

#### Umidade e Vento
| Coluna | Descrição | Unidade | Min/Max |
| :--- | :--- | :--- | :--- |
| Umidade Relativa | Percentual de umidade | % | 10% a 100% |
| Vento Direção | Direção média do vento | Graus | 0 a 360 |
| Vento Velocidade | Velocidade média horária | m/s | 0 a 40 m/s |



### Ranking dos Dias Mais Chuvosos (Aracaju)

| Posição | Data       | Precipitação (mm) |
| :------ | :--------- | :---------------- |
| 1°      | 2024-05-07 | 95.40             |
| 2°      | 2025-05-04 | 92.00             |
| 3°      | 2021-01-30 | 82.40             |
| 4°      | 2025-04-12 | 81.40             |
| 5°      | 2025-05-20 | 74.20             |

