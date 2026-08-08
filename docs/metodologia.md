# Metodologia

## Visão geral

O objetivo é estimar o **déficit habitacional** (metodologia da Fundação João Pinheiro — FJP)
para o estado de São Paulo em **nível de Setor Censitário**, escala em que esse indicador não é
calculável diretamente, pois depende de variáveis do questionário da amostra do Censo — disponível
apenas em nível de **Área de Ponderação (AP)**, uma unidade territorial maior.

> **Nota sobre a base censitária:** a proposta original previa o Censo Demográfico 2022, mas os
> microdados da amostra desse Censo ainda não haviam sido divulgados pelo IBGE no início da
> pesquisa.

O projeto foi conduzido em duas fases, com abordagens distintas:

## Fase 1 — Exploratória (XGBoost)

**Notebook:** [`notebooks/02_AreaDePonderacao_IC.ipynb`](../notebooks/02_AreaDePonderacao_IC.ipynb)

1. Treinar um `XGBRegressor` em cada componente do déficit (domicílios precários, coabitação,
   ônus excessivo, adensamento, déficit total), separadamente para SP Capital e SP Exceto Capital.
2. Testar a aplicação **direta** do modelo aos setores censitários, somando as predições de
   todos os setores de uma AP e comparando com o valor real da FJP para aquela AP.

## Fase 2 — Final (Random Forest + desagregação por propensão)

**Notebook:** [`notebooks/03_SetorCensitario_IC.ipynb`](../notebooks//03_SetorCensitario_IC.ipynb)

1. **Modelagem:** um único `RandomForestRegressor` (200 árvores) é treinado no banco consolidado
   de Áreas de Ponderação (`BD_SP_DEFICIT.xlsx`), usando 68 variáveis do questionário do universo
   como *features* e o `DEFICIT_TOTAL` (FJP) como alvo.
   - Validação: divisão treino/teste 80/20 + validação cruzada 5-fold.
   - Interpretabilidade: SHAP (SHapley Additive exPlanations) e Permutation Importance.
2. **Desagregação espacial por escores de propensão:**
   - O modelo é aplicado aos Setores Censitários (`BANCO_SP_setorcensitario.xlsx`), gerando um
     escore de propensão relativa (não um valor de déficit) para cada setor.
   - Dentro de cada AP, os escores são normalizados (soma = 1) e usados como pesos para
     redistribuir o déficit total, já conhecido, da AP entre seus setores.
   - Essa construção garante, por definição, que a soma dos setores de uma AP reproduz
     exatamente o valor oficial da AP.
3. **Auditoria:** verificação numérica de que a soma dos setores bate com o total da AP
   (diferenças observadas da ordem de 10⁻¹³, compatíveis com erro de ponto flutuante).
4. **Validação espacial:**
   - Índice de Moran Global (autocorrelação espacial da distribuição resultante);
   - LISA (Local Indicators of Spatial Association), para localizar clusters HH/LL/HL/LH;
   - Mapeamento da malha de setores censitários do IBGE.

## Principais resultados numéricos

| Etapa | Métrica | Valor |
|---|---|---|
| Random Forest (AP), validação cruzada 5-fold | R² médio | 0,9234 (± 0,0257) |
| Random Forest (AP), validação cruzada 5-fold | MAE médio | 104,25 (± 37,50) |
| Permutation Importance | Variável mais importante | `Soma_V015` (Outros parentes no domicílio), importância ≈ 0,504 |
| Auditoria da desagregação | Maior diferença absoluta | ~10⁻¹³ (soma dos setores = total da AP) |
| Moran Global | Índice I | 0,524625 (p = 0,001) |
| LISA | Setores em clusters significativos | 42,7% do total (HH: 15,6% · LL: 22,9% · HL: 1,0% · LH: 3,4%) |

## Referências metodológicas centrais

- **FJP** — metodologia oficial de cálculo do déficit habitacional (componentes: domicílios
  precários, coabitação, ônus excessivo com aluguel, adensamento excessivo).
- **Breiman (2001)** — Random Forest.
- **Lundberg & Lee (2017)** — SHAP.
- **Goodchild & Lam (1980)** — Modifiable Areal Unit Problem (MAUP), base conceitual do problema
  de desagregação espacial.
- **Moran (1950)**, **Anselin (1995)** — Índice de Moran Global e LISA.

A lista completa de referências está em [`references/referencias.md`](../references/referencias.md).
