# Análise de Leitos Hospitalares CNES

Análise exploratória da capacidade hospitalar, da oferta de leitos e da cobertura SUS, com foco no município de Santos (SP).

## Sumário

- [Sobre o projeto](#sobre-o-projeto)
- [Escopo da análise](#escopo-da-análise)
- [Resultados](#resultados)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Requisitos](#requisitos)
- [Como executar](#como-executar)
- [Metodologia](#metodologia)
- [Saídas do notebook](#saídas-do-notebook)
- [Limitações conhecidas](#limitações-conhecidas)
- [Próximos passos](#próximos-passos)
- [Licença](#licença)

## Sobre o projeto

O projeto combina um notebook Jupyter e uma planilha Excel com dados hospitalares organizados por competência. A análise usa a competência mais recente para produzir uma fotografia da rede e todas as competências disponíveis para observar a evolução temporal.

O recorte principal é Santos, com comparações agregadas para o estado de São Paulo e o Brasil. O notebook também detalha a distribuição dos leitos por hospital e bairro e identifica pontos de atenção para a gestão pública.

## Escopo da análise

| Item | Descrição |
| --- | --- |
| Foco geográfico | Santos (SP) |
| Comparações | Estado de São Paulo e Brasil |
| Competências | `202601`, `202602` e `202603` |
| Base principal | Aba `Leitos_2026` |
| Registros analisados | 21.602 linhas e 35 colunas |
| Tecnologias | Python, Jupyter, Pandas, NumPy, Matplotlib, Seaborn e OpenPyXL |

## Resultados

Os números abaixo correspondem à competência mais recente disponível: `202603`.

| Indicador | Santos | São Paulo | Brasil |
| --- | ---: | ---: | ---: |
| Estabelecimentos | 17 | 1.021 | 7.188 |
| Leitos existentes | 1.939 | 109.559 | 520.129 |
| Leitos SUS | 814 | 61.863 | 352.552 |
| Cobertura SUS de leitos | 41,98% | 56,47% | 67,78% |
| UTI existente | 341 | 15.562 | 63.773 |
| UTI SUS | 143 | 7.325 | 31.970 |
| Cobertura SUS de UTI | 41,94% | 47,07% | 50,13% |
| UTI sobre leitos | 17,59% | 14,20% | 12,26% |

### Principais achados

- Santos ocupa a 8ª posição entre os municípios paulistas por número de leitos existentes.
- O índice de concentração da oferta é de 1.269 no HHI; aproximadamente oito hospitais concentram 80% dos leitos.
- Dez estabelecimentos possuem leitos existentes e nenhum leito SUS.
- Cinco estabelecimentos possuem UTI instalada e nenhuma UTI SUS.
- A simulação estima 281 leitos SUS adicionais para alcançar a cobertura observada em São Paulo e 500 para alcançar a referência nacional.

## Estrutura do repositório

| Arquivo | Descrição |
| --- | --- |
| [`analise.ipynb`](analise.ipynb) | Notebook com preparação, validação, análise e visualizações. |
| [`hospitais CNES.xlsx`](hospitais%20CNES.xlsx) | Base local em Excel, com as abas `Leitos_2026` e `hospitais CNES`. |

## Requisitos

- Python 3.10 ou superior.
- Jupyter Notebook.
- Pandas, NumPy, Matplotlib, Seaborn e OpenPyXL.
- A planilha `hospitais CNES.xlsx` deve permanecer na raiz do projeto.

## Como executar

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install jupyter pandas numpy matplotlib seaborn openpyxl
.\.venv\Scripts\jupyter.exe notebook analise.ipynb
```

### macOS ou Linux

```bash
python3 -m venv .venv
.venv/bin/python -m pip install --upgrade pip
.venv/bin/python -m pip install jupyter pandas numpy matplotlib seaborn openpyxl
.venv/bin/jupyter notebook analise.ipynb
```

Depois de iniciar o Jupyter, abra `analise.ipynb` e execute as células na ordem. Mantenha o arquivo Excel no mesmo diretório do notebook.

> [!WARNING]
> O notebook salvo atualmente referencia `df_atual`, `df_santos` e `df_santos_atual` antes de definir esses recortes. Depois da célula de normalização de texto, insira o bloco abaixo ou adicione uma célula equivalente ao notebook.

```python
df_atual = df[df["COMP"] == df["COMP"].max()].copy()
df_santos = df[df["MUNICIPIO_NORM"] == "SANTOS"].copy()
df_santos_atual = df_atual[df_atual["MUNICIPIO_NORM"] == "SANTOS"].copy()
```

## Metodologia

1. Carrega a aba `Leitos_2026` da planilha.
2. Verifica nulos, valores negativos, zeros e duplicidades nas colunas numéricas.
3. Normaliza nomes de municípios, bairros e unidades para reduzir problemas de acentuação.
4. Usa a maior competência disponível como fotografia atual da rede.
5. Agrega leitos e UTI por município, hospital e bairro.
6. Compara Santos com São Paulo e Brasil.
7. Calcula a concentração da oferta por HHI e participação acumulada.
8. Simula o volume de leitos SUS necessário para alcançar as referências estadual e nacional.

| Métrica | Fórmula |
| --- | --- |
| Cobertura SUS de leitos | `LEITOS_SUS / LEITOS_EXISTENTES` |
| Cobertura SUS de UTI | `UTI_TOTAL_SUS / UTI_TOTAL_EXIST` |
| UTI sobre leitos | `UTI_TOTAL_EXIST / LEITOS_EXISTENTES` |
| HHI de leitos | Soma dos quadrados das participações percentuais por hospital |

## Saídas do notebook

O notebook gera tabelas e gráficos para:

- evolução mensal de leitos e UTI em Santos;
- comparação entre Santos, São Paulo e Brasil;
- ranking de municípios paulistas por leitos existentes;
- análise individual dos hospitais de Santos;
- concentração da oferta e curva de Pareto;
- perfil de UTI por subtipo;
- distribuição territorial por bairro;
- gaps de leitos e UTI não SUS;
- matriz de risco por porte hospitalar e cobertura SUS;
- variação entre competências e auditoria de dados cadastrais.

## Limitações conhecidas

- A base contém apenas as competências `202601`, `202602` e `202603`; a série ainda não representa uma tendência histórica longa.
- Os indicadores medem capacidade cadastrada, não ocupação, produção hospitalar, tempo de permanência ou demanda reprimida.
- O notebook contém uma célula com `NameError` por falta das definições dos recortes `df_atual`, `df_santos` e `df_santos_atual`.
- A planilha inclui campos de contato, como `NU_TELEFONE` e `NO_EMAIL`; revise os dados antes de publicar ou compartilhar o arquivo.
- O repositório não contém script de download, dicionário de dados ou metadados de atualização da base.

## Próximos passos

- Corrigir o fluxo de preparação do notebook e adicionar um arquivo de dependências reproduzível.
- Documentar a origem, a data de extração e o dicionário de dados da planilha.
- Integrar população por faixa etária para calcular leitos por 1.000 habitantes.
- Incorporar uma série histórica de 12 meses ou mais.
- Cruzar capacidade com internações, permanência e ocupação.

## Licença

Nenhuma licença foi definida no repositório atual. Consulte os responsáveis antes de redistribuir o código, o notebook ou a base de dados.
