# IA Aplicada à Estimativa do Déficit Habitacional — Abordagem Multiescalar do Estado de São Paulo

Projeto de Iniciação Científica (PIBITI/PROPQ) desenvolvido na **Universidade Federal de São
Carlos (UFSCar)**, Programa de Pós-Graduação em Engenharia Urbana (PPGEU), vinculado ao grupo de
pesquisa **Cidades e Pessoas Conectadas**.

**Bolsista:** Griselda Karen Sillerico Justo
**Orientadora:** Profa. Dra. Elza Luli Miyasaka
**Co-orientadoras:** Dra. Tatiane Ferreira Olivatto · Me. Priscila Kauana Barelli Forcel

---

## Resumo do projeto

O déficit habitacional é tradicionalmente calculado pela metodologia da **Fundação João Pinheiro
(FJP)** em nível de **Área de Ponderação (AP)** — a menor unidade geográfica para a qual o
questionário da amostra do Censo Demográfico é representativo. Isso limita a identificação de
desigualdades habitacionais dentro das cidades, já que uma AP pode agrupar centenas de domicílios
com realidades muito diferentes entre si.

Este projeto usa **aprendizado de máquina** para desagregar essa estimativa para o nível de
**Setor Censitário (SC)** no estado de São Paulo. A
abordagem final combina:

1. Um modelo **Random Forest**, treinado nas Áreas de Ponderação, para aprender a relação entre
   variáveis do Censo (habitação, infraestrutura, composição familiar, renda) e o déficit
   habitacional total (FJP);
2. Uma etapa de **desagregação espacial baseada em escores de propensão**, que usa esse modelo
   para redistribuir — sem alterar — o valor já conhecido de cada AP entre seus setores
   censitários, de forma proporcional à propensão relativa de cada um;
3. Validação por **interpretabilidade** (SHAP, Permutation Importance) e por **autocorrelação
   espacial** (Índice de Moran Global, LISA), para checar se o resultado final é estatisticamente
   consistente e espacialmente plausível.

## Estrutura do repositório

```
.
├── README.md                      <- este arquivo
│
├── data/
│   └── README.md/ 
│   └── area_de_ponderacao/                  <- Bases de dados usada na etapa 1
│   │   ├── BANCO_SP_EXCETOCAPITAL.xlsx              
│   │   ├── BANCO_SP_EXCETOCAPITAL_setorcensitario.xlsx    
│   │   ├── BANCO_SPCAPITAL.xlsx        
│   │   └── BANCO_SPCAPITAL_setorcensitario.xlsx       
│   └── setores_censitarios/                  <- Bases de dados usada na etapa 2
│   │   ├── BD_SP_DEFICIT.xlsx               
│   │   ├── BANCO_SP_setorcensitario.xlsx    
│   │   └── SP_setores_CD2022.zip       
│
├── notebooks/
│   ├── 01_conceitos_teoricos.ipynb
│   ├── 02_area_ponderacao_xgboost.ipynb         <- Fase exploratória (XGBoost) 
│   └── 03_setor_censitario_desagregacao.ipynb   <- Fase final             
│
├── docs/
│   ├── metodologia.md              <- resumo metodológico das duas fases
│   └── DICIONARIO VARIAVEIS.xlsx              <- dicionário de variáveis
│
├── references/
│   └── referencias.md              <- bibliografia do projeto
│
└── results/
    └── figures/                    <- principais gráficos e mapas gerados (imagens finais)
```

## Como reproduzir

### 1. Ordem de execução

1. `notebooks/01_conceitos_teoricos.ipynb` *(opcional, mas recomendado)* — explica as técnicas
   usadas antes de mexer nos dados reais.
2. `notebooks/02_area_ponderacao_xgboost.ipynb` *(opcional)* — documenta a fase exploratória e por
   que a abordagem mudou.
3. `notebooks/03_setor_censitario_desagregacao.ipynb` — pipeline final, do carregamento dos dados
   ao mapa final do déficit desagregado.

## Metodologia (resumo)

Ver [`docs/metodologia.md`](docs/metodologia.md) para o detalhamento completo. Em síntese:

1. **Random Forest** treinado nas Áreas de Ponderação → prevê o déficit habitacional total a
   partir de 68 variáveis do Censo.
2. O mesmo modelo, aplicado aos Setores Censitários, gera **escores de propensão relativa**
   (não um valor de déficit).
3. Dentro de cada AP, os escores são normalizados e usados como **pesos** para redistribuir o
   valor total, já conhecido, da AP entre seus setores — preservando exatamente esse total.
4. A qualidade do modelo e da desagregação é validada por métricas de regressão, técnicas de
   interpretabilidade (SHAP, Permutation Importance) e autocorrelação espacial (Moran, LISA).

## Relatórios completos

Os relatórios completos do projeto (proposta de pesquisa, relatório parcial e relatório final,
com toda a revisão bibliográfica e discussão teórica) **não fazem parte deste repositório**. A
bibliografia consolidada está disponível em [`references/referencias.md`](references/referencias.md)
e o resumo metodológico em [`docs/metodologia.md`](docs/metodologia.md).

## Limitações 

- A desagregação por propensão depende da qualidade do modelo de Área de Ponderação; ela garante
  consistência agregada (a soma bate com o total conhecido), mas não garante que a distribuição
  *dentro* de cada AP seja perfeita, por isso a validação espacial (Moran/LISA) é parte
  essencial da metodologia, não apenas um extra.
- **Base censitária:** a proposta original previa o uso do Censo Demográfico 2022, mas os
  microdados da amostra desse Censo ainda não haviam sido divulgados pelo IBGE no início da
  pesquisa. Por isso, a modelagem final (Random Forest +
  desagregação por propensão, notebook 03) foi desenvolvida com o **Censo Demográfico de 2010**,
  enquanto o teste exploratório com XGBoost (notebook 02) já incorporava dados mais recentes
  conforme iam sendo liberados. Uma atualização natural do projeto é reexecutar o pipeline final
  com os microdados do Censo 2022 assim que integralmente disponíveis.

## Tecnologias

Python · pandas · scikit-learn · XGBoost · Random Forest · SHAP · GeoPandas · libpysal · esda · splot ·
matplotlib · seaborn


## Agradecimentos

Ao grupo de pesquisa **Cidades e Pessoas Conectadas** (UFSCar/PPGEU), pela orientação teórica e
metodológica ao longo do projeto, e ao Programa Institucional de Bolsas de Iniciação em
Desenvolvimento Tecnológico e Inovação (PIBITI/PROPQ-UFSCar).
