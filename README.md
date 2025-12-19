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

- Variáveis Temporais
  
Data: Data da observação meteorológica.

Hora UTC: Hora da medição, expressa no fuso horário UTC, com registros horários ao longo do dia.

- Precipitação
  
PRECIPITAÇÃO TOTAL, HORÁRIO (mm): Volume total de precipitação acumulada durante a hora de observação, medido em milímetros (mm).

- Pressão Atmosférica

PRESSÃO ATMOSFÉRICA AO NÍVEL DA ESTAÇÃO, HORÁRIA (mB): Valor da pressão atmosférica medida ao nível da estação meteorológica, registrado de forma horária.

PRESSÃO ATMOSFÉRICA MÁXIMA NA HORA ANTERIOR (AUT) (mB): Maior valor de pressão atmosférica registrado na hora anterior à observação, obtido automaticamente.

PRESSÃO ATMOSFÉRICA MÍNIMA NA HORA ANTERIOR (AUT) (mB): Menor valor de pressão atmosférica registrado na hora anterior à observação, obtido automaticamente.

- Radiação Solar
  
RADIAÇÃO GLOBAL (kJ/m²): Quantidade total de radiação solar incidente na superfície durante o período de observação, expressa em quilojoules por metro quadrado.

- Temperatura do Ar
  
TEMPERATURA DO AR – BULBO SECO, HORÁRIA (°C): Temperatura do ar medida diretamente pelo sensor, registrada de forma horária.

TEMPERATURA MÁXIMA NA HORA ANTERIOR (AUT) (°C): Maior valor de temperatura do ar registrado na hora anterior à observação.

TEMPERATURA MÍNIMA NA HORA ANTERIOR (AUT) (°C): Menor valor de temperatura do ar registrado na hora anterior à observação.

- Ponto de Orvalho
  
TEMPERATURA DO PONTO DE ORVALHO (°C): Temperatura na qual o ar atinge a saturação de umidade, indicando a formação de condensação.

TEMPERATURA DO ORVALHO MÁXIMA NA HORA ANTERIOR (AUT) (°C): Maior valor da temperatura do ponto de orvalho registrado na hora anterior.

TEMPERATURA DO ORVALHO MÍNIMA NA HORA ANTERIOR (AUT) (°C): Menor valor da temperatura do ponto de orvalho registrado na hora anterior.

- Umidade Relativa do Ar
  
UMIDADE RELATIVA DO AR, HORÁRIA (%): Percentual de umidade relativa do ar medido no momento da observação.

UMIDADE RELATIVA MÁXIMA NA HORA ANTERIOR (AUT) (%): Maior valor de umidade relativa registrado na hora anterior.

UMIDADE RELATIVA MÍNIMA NA HORA ANTERIOR (AUT) (%)> Menor valor de umidade relativa registrado na hora anterior.

- Vento
  
VENTO, DIREÇÃO HORÁRIA (graus): Direção média do vento durante o período de observação, expressa em graus.

VENTO, RAJADA MÁXIMA (m/s): Velocidade máxima de rajada de vento registrada na hora anterior.

VENTO, VELOCIDADE HORÁRIA (m/s): Velocidade média do vento registrada de forma horária.

# Desenvolvimento

Este MVP foi desenvolvido como parte da disciplina de Engenharia de Dados, com foco na validação de um pipeline mínimo, funcional e escalável, utilizando dados reais e aplicando boas práticas de organização, processamento distribuído e análise de dados em nuvem.
