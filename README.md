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

3. Catálogo de Dados
   
| Coluna                                               | Mínimo | Máximo | Dados faltantes | Total de registros |
|------------------------------------------------------|--------|--------|-----------------|--------------------|
| precipitao_total_horrio_mm                            | 0      | 48.6   | 10744           | 40896              |
| pressao_atmosferica_ao_nivel_da_estacao_horaria_mb   | 1002.8 | 1024.2 | 10786           | 40896              |
| presso_atmosferica_max_na_hora_ant_aut_mb            | 1003.4 | 1030.1 | 8100            | 40896              |
| presso_atmosferica_min_na_hora_ant_aut_mb            | 995.7  | 1022.8 | 8100            | 40896              |
| radiacao_global_kj_m                                 | 0      | 3253.9 | 23143           | 40896              |
| temperatura_do_ar_bulbo_seco_horaria_c               | 19.7   | 39.4   | 18322           | 40896              |
| temperatura_do_ponto_de_orvalho_c                    | -9.2   | 34.7   | 27433           | 40896              |
| temperatura_mxima_na_hora_ant_aut_c                  | 19.9   | 36.4   | 18145           | 40896              |
| temperatura_mnima_na_hora_ant_aut_c                  | 18.1   | 36.8   | 15678           | 40896              |
| temperatura_orvalho_max_na_hora_ant_aut_c            | -9.1   | 35.1   | 27501           | 40896              |
| temperatura_orvalho_min_na_hora_ant_aut_c            | -9.8   | 28.6   | 27517           | 40896              |
| umidade_rel_max_na_hora_ant_aut                       | 8      | 100    | 19905           | 40896              |
| umidade_rel_min_na_hora_ant_aut                       | 8      | 100    | 19926           | 40896              |
| umidade_relativa_do_ar_horaria                       | 7      | 100    | 21079           | 40896              |
| vento_direo_horaria_gr_gr                            | 1      | 360    | 10744           | 40896              |
| vento_rajada_maxima_m_s                              | 0.7    | 20.3   | 10744           | 40896              |
| vento_velocidade_horaria_m_s                         | 0.1    | 6.5    | 10744           | 40896              |
| precipitao_total_mm                                  | 0      | 32     | 38252           | 40896              |
| pressao_atmosferica_ao_nivel_da_estacao_mb           | 1002.7 | 1019.4 | 38252           | 40896              |
| temperatura_do_ar_bulbo_seco_c                       | 21.1   | 31.1   | 38252           | 40896              |
| umidade_relativa_do_ar                               | 14     | 100    | 39659           | 40896              |
| vento                                                | 2      | 360    | 38252           | 40896              |
| vento_maxima_m_s                                     | 1.4    | 12.3   | 38252           | 40896              |
| vento_velocidade_m_s                                 | 0.3    | 6      | 38252           | 40896              |

Os dados acima compõem a camada Silver/Gold do Data Lake. Optou-se por um modelo Flat (Tabela Fato Desnormalizada), visto que em análises de séries temporais meteorológicas, a performance de leitura e a integridade cronológica são priorizadas em relação à normalização excessiva de dimensões.

4. Carga

A etapa de carga foi realizada utilizando o poder de processamento distribuído do Apache Spark dentro da plataforma Databricks. O pipeline seguiu o fluxo de Extração, Transformação e Carga (ETL) para garantir que os dados brutos fossem convertidos em um formato otimizado para consulta.

Processo de ETL e Transformação
A documentação do processo de transformação e carga seguiu os seguintes passos:

Ingestão (Extract): Leitura dos arquivos .csv extraídos dos pacotes .zip do INMET. Os dados foram carregados inicialmente em um DataFrame Spark, preservando o esquema original.

Filtragem e Seleção: Como o conjunto de dados original continha registros de todo o território nacional (584 arquivos por ano), foi aplicada uma transformação de filtragem para isolar apenas a estação meteorológica de Aracaju - SE.

Limpeza e Conversão (Transform):

Tipagem de Dados: Conversão de colunas de texto para formatos numéricos (Double) e temporais (Timestamp).

Tratamento de Nulos: Identificação e tratamento do valor -9999 (padrão do INMET para dados ausentes), convertendo-os em null para evitar distorções nas métricas de mínimo e máximo.

Normalização: Ajuste das colunas de data e hora para um formato único, permitindo a ordenação correta para o ranking de precipitação.

Carga Final (Load): Os dados processados foram salvos no Data Lake em formato Parquet/Delta. Essa escolha técnica garante alta performance para consultas analíticas e compressão eficiente dos arquivos.

Conciliação de Dados
Para compor o ranking dos dias mais chuvosos e o catálogo de domínios, foi realizada a conciliação dos conjuntos de dados anuais (2021 a 2025).

Técnica: Utilizou-se a união (Union) dos DataFrames anuais, seguida de uma agregação por data para consolidar a precipitação total diária, já que os dados originais são registrados de forma horária. Essa transformação foi essencial para validar a consistência histórica entre os diferentes arquivos baixados.



### Ranking dos Dias Mais Chuvosos (Aracaju)

| Posição | Data       | Precipitação (mm) |
| :------ | :--------- | :---------------- |
| 1°      | 2024-05-07 | 95.40             |
| 2°      | 2025-05-04 | 92.00             |
| 3°      | 2021-01-30 | 82.40             |
| 4°      | 2025-04-12 | 81.40             |
| 5°      | 2025-05-20 | 74.20             |

