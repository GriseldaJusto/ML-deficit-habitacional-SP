# Dados brutos

| Arquivo | Descrição |
|---|---|
| `BD_SP_DEFICIT.xlsx` | Banco consolidado por Área de Ponderação (treino do modelo). 84 colunas: 10 de identificação geográfica, 68 features do Censo (universo) e 5 componentes do déficit habitacional (metodologia FJP). Ver `docs/dicionario_variaveis.md`. |
| `BANCO_SP_setorcensitario.xlsx` | Banco por Setor Censitário (aplicação do modelo). Mesmas variáveis explicativas do Censo, com nomes de coluna por extenso (tratados na etapa de padronização do notebook 02). |
| `dicionario_variaveis.xlsx` | Dicionário completo de variáveis (fonte da versão em Markdown `docs/dicionario_variaveis.md`). |

## Não incluído neste repositório

- **Malha de setores censitários do IBGE** (shapefile), necessária apenas na parte final do
  notebook `02` (mapas, Índice de Moran, LISA). Baixe o shapefile do estado de São Paulo
  (Censo 2022) em:
  <https://www.ibge.gov.br/geociencias/organizacao-do-territorio/malhas-territoriais/26565-malhas-de-setores-censitarios-divisoes-intramunicipais.html>
  e salve como `SP_setores_CD2022.zip` nesta pasta.
- **`BANCO_SPCAPITAL.xlsx` / `BANCO_SP_EXCETOCAPITAL.xlsx`** e seus equivalentes por setor —
  insumos brutos usados apenas no notebook exploratório `01`, anteriores à consolidação em
  `BD_SP_DEFICIT.xlsx`.
