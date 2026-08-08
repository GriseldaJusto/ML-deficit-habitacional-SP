# Dicionário de Variáveis

Este documento descreve todas as colunas presentes nos bancos de dados do projeto
(`data/raw/BD_SP_DEFICIT.xlsx` e `data/raw/BANCO_SP_setorcensitario.xlsx`), organizadas em três
grupos. A fonte original está em `data/raw/dicionario_variaveis.xlsx`.

> Os códigos `Soma_V0XX` seguem a nomenclatura de variáveis do questionário do universo do
> Censo Demográfico do IBGE. O sufixo `.x` / `.y` / `.x.x` aparece quando a mesma variável (`VXXX`)
> existe em mais de uma tabela de origem do Censo e precisou ser diferenciada após a junção dos
> dados (é um artefato do `pandas.merge`, não tem significado semântico).

## 1. Variáveis de identificação geográfica (10 colunas)

Presentes apenas no banco de Área de Ponderação; identificam a localização de cada linha
(UF, mesorregião, microrregião, região metropolitana e município).

| Código | Descrição | Planilha de origem |
|---|---|---|
| `AREA_POND` | Área de Ponderação | - |
| `Cod_UF` | Cód. UF | - |
| `Nome_da_UF` | UF | - |
| `Nome_da_meso` | Mesorregião | - |
| `Cod_micro` | Cód. Microrregião | - |
| `Nome_da_micro` | Microrregião | - |
| `Cod_RM` | Cod_RM | - |
| `Nome_da_RM` | Região Metropolitana | - |
| `Cod_municipio` | Cód. Município | - |
| `Nome_do_municipio` | Município | - |

## 2. Variáveis explicativas — *features* do modelo (68 colunas)

Correspondem às colunas 12 a 79 do banco de Área de Ponderação (`FEATURES` nos notebooks).
Descrevem características habitacionais, de infraestrutura urbana, demográficas e de composição
familiar, extraídas do questionário do universo do Censo 2022. É este conjunto de variáveis que
alimenta o Random Forest e é usado tanto no treino (Área de Ponderação) quanto na aplicação
(Setor Censitário).

| Código | Descrição | Planilha de origem |
|---|---|---|
| `Soma_V002.x` | Domicílios particulares permanentes (=DPP) | 6.2 |
| `Soma_V023.x` | Domicílios particulares permanentes sem banheiro de uso exclusivo dos moradores e nem sanitário | 6.2 |
| `Soma_V037` | Domicílios particulares permanentes com lixo coletado em caçamba de serviço de limpeza | 6.2 |
| `Soma_V038` | Domicílios particulares permanentes com lixo queimado na propriedade | 6.2 |
| `Soma_V039` | Domicílios particulares permanentes com lixo enterrado na propriedade | 6.2 |
| `Soma_V040` | Domicílios particulares permanentes com lixo jogado em terreno baldio oulogradouro | 6.2 |
| `Soma_V041.x` | Domicílios particulares permanentes com lixo jogado em rio, lago ou mar | 62 |
| `Soma_V046` | Domicílios particulares permanentes sem energia elétrica | 6.2 |
| `Soma_V101` | Domicílios particulares permanentes do tipo casa próprios e em aquisição | 6.2 |
| `Soma_V102` | Domicílios particulares permanentes do tipo casa alugados | 6.2 |
| `Soma_V103` | Domicílios particulares permanentes do tipo casa cedidos por empregador | 6.2 |
| `Soma_V233` | Domicílios particulares permanentes com outra forma de destino do lixo e outra forma de abastecimento de água | 6.2 |
| `Soma_V007.x` | Moradores em domicílios particulares permanentes próprios e em aquisição | 6.3 |
| `Soma_V008.x` | Moradores em domicílios particulares permanentes alugados | 6.3 |
| `Soma_V009.x` | Moradores em domicílios particulares permanentes cedidos por empregador | 6.3 |
| `Soma_V011.x` | Moradores em domicílios particulares permanentes com outra condição de ocupação (não são próprios, alugados, nem cedidos) | 6.3 |
| `Soma_V023.y` | Moradores em domicílios particulares permanentes sem banheiro de uso exclusivo dos moradores e nem sanitário | 6.3 |
| `Soma_V041.y` | Moradores em domicílios particulares permanentes sem energia elétrica | 6.3 |
| `Soma_V001.x` | Pessoas responsáveis, do sexo feminino | 6.4 |
| `Soma_V109` | Pessoas responsáveis, do sexo masculino | 6.5 |
| `Soma_V001.y` | Pessoas Residentes | 6.8 |
| `Soma_V002.y` | Pessoas Residentes e cor ou raça - branca | 6.8 |
| `Soma_V003.x` | Pessoas Residentes e cor ou raça - preta | 6.8 |
| `Soma_V004.x` | Pessoas Residentes e cor ou raça - amarela | 6.8 |
| `Soma_V005.x` | Pessoas Residentes e cor ou raça - parda | 6.8 |
| `Soma_V006.x` | Pessoas Residentes e cor ou raça - indígena | 6.8 |
| `Soma_V002.x.x` | Pessoas residentes em domicílios particulares permanentes | 6.16 |
| `Soma_V003.y` | Responsáveis pelos domicílios particulares | 6.16 |
| `Soma_V004.y` | Cônjuges ou companheiros(as) (de sexo diferente e do mesmo sexo da pessoa responsável) em domicílios particulares | 6.16 |
| `Soma_V005.y` | Filhos(as) do responsável e do cônjuge em domicílios particulares | 6.16 |
| `Soma_V006.y` | Filhos(as) somente do responsável em domicílios particulares | 6.16 |
| `Soma_V007.y` | Enteados(as) em domicílios particulares | 6.16 |
| `Soma_V008.y` | Genros ou noras em domicílios particulares | 6.16 |
| `Soma_V009.y` | Pais, mães, padrastos ou madrastas em domicílios particulares | 6.16 |
| `Soma_V010` | Sogros (as) em domicílios particulares | 6.16 |
| `Soma_V011.y` | Netos(as) em domicílios particulares | 6.16 |
| `Soma_V012` | Bisnetos(as) em domicílios particulares | 6.16 |
| `Soma_V013` | Irmãos ou irmãs em domicílios particulares | 6.16 |
| `Soma_V014.x` | Avôs ou avós em domicílios particulares | 6.16 |
| `Soma_V015` | Outros parentes em domicílios particulares | 6.16 |
| `Soma_V016` | Agregados(as) em domicílios particulares | 6.16 |
| `Soma_V017.x` | Conviventes em domicílios particulares | 6.16 |
| `Soma_V001` | Total de domicílios particulares improvisados | 6.19 |
| `Soma_V002.y.y` | Total do rendimento nominal mensal dos domicílios particulares | 6.19 |
| `Soma_V004` | Total do rendimento nominal mensal dos domicílios particulares improvisados | 6.19 |
| `Soma_V014.y` | Domicílios particulares sem rendimento nominal mensal domiciliar per capita | 6.19 |
| `Soma_V011` | Domicílios particulares permanentes alugados – Não existe iluminação pública | 6.22 |
| `Soma_V017.y` | Domicílios particulares permanentes alugados – Não existe pavimentação | 6.22 |
| `Soma_V050` | Domicílios particulares permanentes próprios – Existe esgoto a céu aberto | 6.22 |
| `Soma_V052` | Domicílios particulares permanentes alugados – Existe esgoto a céu aberto | 6.22 |
| `Soma_V113` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe iluminação pública | 6.22 |
| `Soma_V119` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe pavimentação | 6.22 |
| `Soma_V125` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe calçada | 6.22 |
| `Soma_V131` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe meio-fio/guia | 6.22 |
| `Soma_V137` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe bueiro/boca-de-lobo | 6.22 |
| `Soma_V143` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe rampa para cadeirante | 6.22 |
| `Soma_V149` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Não existe arborização | 6.22 |
| `Soma_V154` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Existe esgoto a céu aberto | 6.22 |
| `Soma_V160` | Domicílios particulares permanentes que não tinham banheiro ou sanitário – Existe lixo acumulado nos logradouros | 6.22 |
| `Soma_V202` | Domicílios particulares permanentes com moradia adequada – Existe identificação do logradouro | 6.23 |
| `Soma_V203` | Domicílios particulares permanentes com moradia adequada – Não existe identificação do logradouro | 6.23 |
| `Soma_V204` | Domicílios particulares permanentes com moradia semi-adequada – Existe identificação do logradouro | 6.23 |
| `Soma_V205` | Domicílios particulares permanentes com moradia semi-adequada – Não existe identificação do logradouro | 6.23 |
| `Soma_V206` | Domicílios particulares permanentes com moradia inadequada –  Existe identificação do logradouro | 6.23 |
| `Soma_V207` | Domicílios particulares permanentes com moradia inadequada – Não existe identificação do logradouro | 6.23 |
| `Soma_soma_V202eV203` | Moradia Adequada_V202eV203 | - |
| `Soma_soma_V204eV205` | Moradia Semi-Adequada_V204eV205 | - |
| `Soma_soma_V206eV207` | Moradia Inadequada_V206eV207 | - |

## 3. Variáveis-alvo — componentes do déficit habitacional (5 colunas)

Calculadas segundo a metodologia da Fundação João Pinheiro (FJP), disponíveis **apenas** no
banco de Área de Ponderação (`SAIDAS` nos notebooks). É a partir delas que o modelo aprende a
relação entre características do território e necessidade habitacional.

| Código | Descrição | Planilha de origem |
|---|---|---|
| `DOMICILIOS_PRECARIOS` | DOMICILIOS_PRECARIOS | DÉFICIT CALCULADO POR ÁREA DE PONDERAÇÃO |
| `COABITACAO` | COABITACAO | - |
| `ONUS_EXCESSIVO` | ONUS EXCESSIVO | - |
| `ADENSAMENTO` | ADENSAMENTO | - |
| `DEFICIT_TOTAL` | DEFICIT TOTAL | - |

## Variáveis mais relevantes segundo SHAP e Permutation Importance

Estas cinco variáveis concentram a maior parte da capacidade preditiva do modelo final (ver
`notebooks/02_setor_censitario_desagregacao.ipynb`, seção *Interpretabilidade*):

| Código | Descrição |
|---|---|
| `Soma_V015` | Outros parentes em domicílios particulares |
| `Soma_V006.y` | Filhos(as) somente do responsável em domicílios particulares |
| `Soma_V102` | Domicílios particulares permanentes do tipo casa alugados |
| `Soma_V011.y` | Netos(as) em domicílios particulares |
| `Soma_V008.y` | Genros ou noras em domicílios particulares |
