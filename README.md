# Dinâmica de Desinformação em Processos Eleitorais: Modelo SEIR ABM

**Artigo científico** — versão condensada em português (≤ 30 páginas), pronta para Overleaf.

## Arquivo principal
- `overleaf.v2.tex` — artigo completo, standalone, sem `\input{}` externos.

## Dependências LaTeX (pacotes utilizados)
```
inputenc, fontenc, babel, graphicx, amsmath, amssymb, amsthm,
booktabs, float, geometry, caption, subcaption, xcolor, enumitem,
natbib, array, multirow, tabularx, hyperref, doi
```

## Figuras necessárias (pasta `../figures/` e `../figures_countries/`)
| Arquivo | Gerado por |
|---|---|
| `figures/fig_hero_comparacao.png` | `analise_resultados.py` |
| `figures_countries/fig_infection_comparison.png` | `analise_paises.py` |

## Referências bibliográficas
- `../references.bib` — BibTeX com todas as referências (>100 entradas).

## Como compilar
```bash
pdflatex overleaf.v2.tex
bibtex overleaf.v2
pdflatex overleaf.v2.tex
pdflatex overleaf.v2.tex
```
Ou suba apenas `overleaf.v2.tex` no Overleaf (único arquivo .tex necessário).

## Replicação do modelo computacional
O modelo ABM está na pasta raiz do projeto (`../`):

| Script | Função |
|---|---|
| `model.py` | Mesa 4.0 — FakeNewsModel |
| `agents.py` | 4 tipos de agentes (Eleitor, Influenciador, Bot, Verificador) |
| `config.py` | Parâmetros (Brasil + 9 países) |
| `batch_run_paises.py` | 1800 simulações cross-country |
| `analise_paises.py` | Figuras + tabelas LaTeX cross-country |
| `sensibilidade_paises.py` | Análise de sensibilidade Tier 3 |

### Ambiente Python
```bash
pip install mesa==4.0 networkx numpy pandas scipy sympy matplotlib
python batch_run_paises.py   # ~56 min CPU, gera CSV em resultados_paises_30reps/
python analise_paises.py     # gera figuras em figures_countries/
```

### Verificações matemáticas
```
overleaf/verification_proofs/verificacao_completa.wl   # Wolfram Language (30/30 OK)
overleaf/verification_proofs/derivacao_beta_seir.py    # SymPy (confirma tudo)
overleaf/verification_proofs/derivacao_R0_paises.py    # R0 por país via SymPy
```

## Parâmetros principais
| Símbolo | Valor | Significado |
|---|---|---|
| N | 1.000 | Agentes totais |
| T | 100 | Dias de campanha |
| β | 0,30 | Taxa de transmissão base |
| R₀_eff | 30/11 ≈ 2,73 | Reprodução efetiva (com bots) |
| R₀_hum | 8/11 ≈ 0,73 | Reprodução humano-a-humano (Brasil) |
| R₀_comb | 0,31 | Reprodução sob política combinada |
| Bots | 7% (base) | Proporção de bots |

## Países analisados (10)
Brasil (Tier 1), México, Argentina, Colômbia, Chile (Tier 2),
Peru, Venezuela, Equador, Bolívia, Uruguai (Tier 3).

## Submissão alvo
JASSS — Journal of Artificial Societies and Social Simulation (open access, indexado no RePEc).
