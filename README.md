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
   
| Variável (Coluna)                      | Mínimo | Máximo | Dados Faltantes | Total de Registros |
|---------------------------------------|--------|--------|-----------------|------------------|
| Vento: Direção (Gr)                   | 1.0    | 360.0  | 8100            | 40896            |
| Umidade Relativa do Ar                 | 7.0    | 100.0  | 19842           | 40896            |
| Umidade Mínima (Hora Ant.)             | 8.0    | 100.0  | 19926           | 40896            |
| Umidade Máxima (Hora Ant.)             | 8.0    | 100.0  | 19905           | 40896            |
| Temp. Orvalho Mínima                    | -9.8   | 28.6   | 27517           | 40896            |
| Temp. Orvalho Máxima                    | -9.1   | 35.1   | 27501           | 40896            |
| Temperatura Máxima (Hora Ant.)         | 19.9   | 36.4   | 18145           | 40896            |
| Temperatura Mínima (Hora Ant.)         | 18.1   | 36.8   | 15678           | 40896            |
| Temperatura do Ponto de Orvalho        | -9.2   | 34.7   | 27433           | 40896            |
| Temperatura do Ar (°C)                 | 19.7   | 39.4   | 15678           | 40896            |
| Radiação Global (kJ/m²)               | 0.0    | 3253.9 | 23143           | 40896            |
| Pressão Atmosf. Mínima                 | 995.7  | 1022.8 | 8100            | 40896            |
| Pressão Atmosf. Máxima                 | 1003.4 | 1030.1 | 8100            | 40896            |
| Pressão Atmosférica (mb)               | 1002.7 | 1024.2 | 8142            | 40896            |
| Precipitação Total (mm)                | 0.0    | 48.6   | 8100            | 40896            |


Os dados acima compõem a camada Silver/Gold do Data Lake. Optou-se por um modelo Flat (Tabela Fato Desnormalizada), visto que em análises de séries temporais meteorológicas, a performance de leitura e a integridade cronológica são priorizadas em relação à normalização excessiva de dimensões.

4. Carga

A etapa de carga foi realizada utilizando o poder de processamento distribuído do Apache Spark dentro da plataforma Databricks. O pipeline seguiu o fluxo de Extração, Transformação e Carga (ETL) para garantir que os dados brutos fossem convertidos em um formato otimizado para consulta.

Processo de ETL e Transformação
A documentação do processo de transformação e carga seguiu os seguintes passos:

- Ingestão : Leitura dos arquivos .csv extraídos dos pacotes .zip do INMET. Os dados foram carregados inicialmente em um DataFrame Spark, preservando o esquema original.

- Filtragem e Seleção: Como o conjunto de dados original continha registros de todo o território nacional (584 arquivos por ano), foi aplicada uma transformação de filtragem para isolar apenas a estação meteorológica de Aracaju - SE.

- Tipagem de Dados: Conversão de colunas de texto para formatos numéricos (Double) e temporais (Timestamp).

- Tratamento de Nulos: Identificação e tratamento do valor -9999 (padrão do INMET para dados ausentes), convertendo-os em null para evitar distorções nas métricas de mínimo e máximo.

- Normalização: Ajuste das colunas de data e hora para um formato único, permitindo a ordenação correta para o ranking de precipitação.

- Carga Final (Load): Os dados processados foram salvos no Data Lake em formato Parquet/Delta. Essa escolha técnica garante alta performance para consultas analíticas e compressão eficiente dos arquivos.
  
5. Análise

- Qualidade de dados
As variáveis medidas neste banco de dados, de modo geral, apresentam limitações de qualidade devido à significativa quantidade de dados faltantes. Na documentação disponível no site de origem, não foi possível identificar explicações detalhadas sobre as causas dessas ausências. Uma exceção plausível é a variável radiação global, cuja elevada taxa de dados faltantes se justifica pelo fato de sua medição depender diretamente da incidência de luz solar, resultando em valores nulos durante os períodos noturnos.

O objetivo deste trabalho é avaliar o ranking dos dias mais chuvosos e dos dias mais frios e mais quentes da cidade de Aracaju. Nesse contexto, a variável precipitação horária apresenta 19,80% de dados faltantes. Embora seja uma das variáveis mais completas, a ausência de quase 20% dos registros indica que o ranking dos dias mais chuvosos pode não incluir aproximadamente 1 em cada 5 horas de medição.

Em relação à temperatura do ar, com taxa de dados faltantes entre 38,33% e 44,36%, as médias térmicas de Aracaju estão sujeitas a um possível viés. Se as lacunas ocorrerem predominantemente em horários de pico (por exemplo, meio-dia), a temperatura máxima registrada (39,4°C) pode estar subestimada, assim como a média calculada. Portanto, embora a base permita análises consistentes, é importante considerar essas limitações ao interpretar os resultados.
Variáveis de Orvalho e Radiação (>56%): O alto índice de nulos nestas colunas inviabiliza análises de séries temporais contínuas, servindo apenas para consultas pontuais onde o dado está disponível.

- Solução do problema
Com esta análise, foi possível calcular o ranking dos 10 dias mais quentes, mais frios e com maior precipitação no período de 2021 a 2025. A partir desses rankings, tornou-se viável inferir padrões de sazonalidade e compreender melhor a ocorrência desses fenômenos na região estudada.
  
| Data       | Precipitação Total do Dia (mm) |
|------------|-------------------------------|
| 2024-05-07 | 95.40                         |
| 2025-05-04 | 92.00                         |
| 2021-01-30 | 82.40                         |
| 2025-04-12 | 81.40                         |
| 2025-05-20 | 74.20                         |
| 2022-10-26 | 73.00                         |
| 2023-05-19 | 71.80                         |
| 2025-08-02 | 70.20                         |
| 2024-04-23 | 64.00                         |
| 2023-05-23 | 61.80                         |

| Data       | Temperatura Máxima do Dia (°C) |
|------------|-------------------------------|
| 2021-03-12 | 30.51                         |
| 2021-03-14 | 30.39                         |
| 2021-03-11 | 30.26                         |
| 2021-02-25 | 30.17                         |
| 2021-03-20 | 30.10                         |
| 2021-02-28 | 30.05                         |
| 2021-02-15 | 29.94                         |
| 2021-02-26 | 29.88                         |
| 2021-03-09 | 29.83                         |
| 2021-02-24 | 29.81                         |

| Data       | Temperatura Mínima do Dia (°C) |
|------------|-------------------------------|
| 2023-07-06 | 22.87                         |
| 2023-07-09 | 23.09                         |
| 2023-07-10 | 23.25                         |
| 2022-11-06 | 23.38                         |
| 2021-07-08 | 23.42                         |
| 2021-07-07 | 23.42                         |
| 2024-08-08 | 23.54                         |
| 2024-05-30 | 23.58                         |
| 2021-07-01 | 23.59                         |
| 2021-08-14 | 23.69                         |

O cruzamento dos rankings de precipitação e temperatura revela um perfil climático bem definido para Aracaju-SE entre 2021 e 2025, ao mesmo tempo em que evidencia os desafios técnicos de integridade dos dados.

No quesito Precipitação, os dados apontam que os eventos mais críticos de chuva ocorrem predominantemente no segundo trimestre do ano (abril e maio), com um recorde de 95.40 mm em um único dia em maio de 2024. É interessante notar que os dias de chuva extrema não necessariamente coincidem com os dias de menor temperatura média, sugerindo que a nebulosidade e a precipitação em Aracaju mantêm o clima ameno, mas não necessariamente "frio" para os padrões locais.

Quanto à Temperatura, os resultados mostram uma "gangorra" térmica sazonal perfeita, validando o processamento do pipeline. Os dias de calor extremo (médias acima de 30°C) estão concentrados exclusivamente no primeiro trimestre (fevereiro e março de 2021), enquanto os dias de frio relativo (médias próximas a 22.8°C) ocorrem no inverno (julho e agosto). Essa separação clara por meses do ano prova que a conciliação dos arquivos anuais no Databricks manteve a cronologia e a lógica física dos fenômenos.

6. Conclusão

Do ponto de vista da Engenharia de Dados, o resumo mais importante é o impacto da qualidade: enquanto o ranking de frio e chuva apresenta dados distribuídos por vários anos (2021 a 2025), o ranking de calor ficou restrito a 2021. Isso sugere que a perda de dados afetou de forma desigual os anos do projeto, possivelmente devido a falhas nos sensores de temperatura máxima nos anos de 2022 em diante. Portanto, os dados relatam uma cidade com chuvas intensas e sazonais e temperaturas estáveis, mas alertam que a precisão total desses rankings é limitada pela disponibilidade dos sensores da estação automática.

Para evoluir este MVP para uma solução de dados escalável e de alta precisão, o projeto focar-se-á em dois pilares principais: Arquitetura Medalhão (Delta Lake) com implementação de um fluxo de dados estruturado em três camadas (Bronze, Silver e Gold). Isto permitirá manter o histórico bruto original, garantir a limpeza e padronização dos esquemas na camada intermédia e disponibilizar tabelas de alta performance, otimizadas para dashboards e análises avançadas na camada final. E a imputação de Dados: utilizando  técnicas estatísticas e algoritmos (como médias móveis ou KNN) para preencher os mais de 40% de dados faltantes identificados nos sensores. Esta melhoria é crucial para reduzir os desvios térmicos e de precipitação, tornando os rankings e as análises de tendências muito mais fiéis à realidade climática de Aracaju.


