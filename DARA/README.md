# pratica-pesquisa — Malária na Amazônia Legal (2016–2019)

Projeto de prática de pesquisa sobre malária no Brasil, com **análise
exploratória** e **mineração de regras de associação**, incluindo a abordagem
**DARA** (Divergent Association Rules Analysis).

Baseado em: Baroni, L.; Salles, R.; et al. *An analysis of malaria in the
Brazilian Legal Amazon using divergent association rules*. Journal of
Biomedical Informatics, 2020. DOI: 10.1016/j.jbi.2020.103512.

## Estrutura

```
pratica-pesquisa/
├── datasets/                      
├── analise_exploratoria/
│   └── analise_consolidada.Rmd  
├── DARA/
│   ├── datasets-malaria/          
│   ├── 1-generate-rules.Rmd        # etapa 1: gera e filtra regras de associação
│   ├── 2-divergent-ranking.Rmd     # etapa 2: ranking divergente por atributo
│   ├── analise_dara.Rmd            # comparação do nº de regras entre abordagens
│   └── README.md
├── Mineracao_Padroes.Rmd           # pipeline Apriori unificado (interface fit_mineracao)
└── pratica-pesquisa.Rproj
```

## Pré-requisitos

- R (≥ 4.x) e RStudio.
- Pacotes (instalados pelos chunks `install` marcados com `eval=FALSE`):
  `tidyverse`, `lubridate`, `arules`, `arulesViz`, `geobr`, `sf`, `scales`,
  `moments`, `skimr`, `stringr`.

Cada `.RData` em `datasets/` contém um objeto chamado `data` (um ano de dados).

## Fluxo de execução

Abra o projeto pelo `pratica-pesquisa.Rproj` (assim o *working directory* fica
na raiz e os caminhos relativos funcionam). Ordem recomendada:

**1. Análise exploratória** — `Analise_exploratoria/analise_exploratoria_malaria.Rmd`
   - Knit ou rode os chunks na ordem.
   - Ajuste o bloco `config` (`DATA_DIR`, `ANOS`) se mudar a localização dos dados.
   - Saída: estatísticas + gráficos (mapa, séries temporais, raça, idade, parasitas).

**2. Mineração de padrões (visão geral)** — `Mineracao_Padroes.Rmd`
   - Demonstra o pipeline Apriori completo via `fit_mineracao()`.
   - Ajuste `config` (`DATA_DIR`, `ANOS`, `COLS`).

**3. Pipeline DARA** (rode na ordem, a partir da pasta `DARA/`):
   1. `1-generate-rules.Rmd`
      - Ajuste o bloco `config` (alvo `RHS_TARGET`, parâmetros do Apriori, filtros).
      - **Saídas:** `dataset.RData` (dados unificados) e `malaria-rules-g5.RData` (regras).
   2. `2-divergent-ranking.Rmd`
      - **Entradas:** `dataset.RData` e `malaria-rules-g5.RData` da etapa 1.
      - Os nomes no `config` desta etapa já casam com as saídas da etapa 1.
      - Saída: ranking divergente impresso por atributo (lista `results`).
   3. `analise_dara.Rmd` *(opcional)*
      - Compara o nº de regras entre arquivos `.RData` de regras já gerados.

> **Dica:** para trocar de dataset ou de alvo, edite só o bloco `config` no topo
> de cada `.Rmd`. Nada mais precisa mudar.

