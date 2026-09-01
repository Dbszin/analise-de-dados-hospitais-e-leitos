<p align="center">
  <strong>📊 INTELIGÊNCIA EM SAÚDE PÚBLICA</strong>
</p>

<h1 align="center">Análise de Leitos Hospitalares CNES</h1>

<p align="center">
  <em>Uma leitura orientada a dados sobre capacidade hospitalar, oferta SUS e risco de acesso em Santos (SP).</em>
</p>

<p align="center">
  <a href="analise.ipynb">📓 Abrir notebook</a>
  &nbsp;·&nbsp;
  <a href="hospitais%20CNES.xlsx">📁 Acessar base</a>
  &nbsp;·&nbsp;
  <a href="#execucao">🚀 Executar análise</a>
</p>

<p align="center">
  <code>RECORTE · SANTOS / SP</code>
  <code>PERÍODO · 202601 → 202603</code>
  <code>FORMATO · JUPYTER + EXCEL</code>
</p>

<table align="center">
  <tr>
    <td align="center" width="140"><strong>17</strong><br><sub>estabelecimentos</sub></td>
    <td align="center" width="140"><strong>1.939</strong><br><sub>leitos existentes</sub></td>
    <td align="center" width="140"><strong>814</strong><br><sub>leitos SUS</sub></td>
    <td align="center" width="140"><strong>341</strong><br><sub>leitos de UTI</sub></td>
  </tr>
</table>

> [!NOTE]
> Os indicadores destacados correspondem à competência mais recente disponível na base: `202603`.

## 🧭 Navegação

<p align="center">
  <a href="#visao-geral">Visão geral</a> ·
  <a href="#resultados">Resultados</a> ·
  <a href="#arquivos">Arquivos</a> ·
  <a href="#execucao">Execução</a> ·
  <a href="#metodologia">Metodologia</a> ·
  <a href="#limitacoes">Limitações</a>
</p>

## ✨ O que você encontra aqui

- **Visão executiva:** transforma registros hospitalares em indicadores para apoiar decisões de gestão pública em saúde.
- **Leitos e UTI:** compara capacidade instalada, oferta SUS e participação de UTI sobre o total de leitos.
- **Benchmark regional:** posiciona Santos frente ao estado de São Paulo e ao Brasil.
- **Recorte territorial:** detalha a distribuição da oferta por hospital e bairro.
- **Diagnóstico de risco:** evidencia gaps de leitos SUS, concentração da oferta e possíveis fragilidades cadastrais.
- **Storytelling visual:** gera gráficos de evolução, Pareto, matriz de risco, heatmap e composição SUS versus não SUS.

<a id="visao-geral"></a>
## 🏥 Visão geral

O projeto combina um notebook Jupyter e uma planilha Excel com dados hospitalares organizados por competência. A análise seleciona a competência mais recente para produzir uma fotografia da rede e usa todas as competências disponíveis para observar a evolução temporal.

O recorte principal é Santos, com comparações agregadas para São Paulo e Brasil. O material foi estruturado para leitura técnica e apresentação executiva, aproximando capacidade instalada, acesso público e riscos de concentração da oferta.

### 🔎 Perguntas orientadoras

<table>
  <tr>
    <td>🛏️ <strong>Capacidade</strong><br><sub>Quantos leitos e UTIs estão cadastrados?</sub></td>
    <td>🟢 <strong>Acesso SUS</strong><br><sub>Qual parcela da capacidade está disponível ao SUS?</sub></td>
    <td>⚠️ <strong>Risco</strong><br><sub>Onde estão os gaps e as concentrações críticas?</sub></td>
  </tr>
</table>

<a id="resultados"></a>
## 📌 Resultados em um olhar

### Santos frente às referências

| Indicador | Santos | São Paulo | Brasil |
| --- | ---: | ---: | ---: |
| Estabelecimentos | 17 | 1.021 | 7.188 |
| Leitos existentes | 1.939 | 109.559 | 520.129 |
| Leitos SUS | 814 | 61.863 | 352.552 |
| Cobertura SUS de leitos | **41,98%** | 56,47% | 67,78% |
| UTI existente | 341 | 15.562 | 63.773 |
| UTI SUS | 143 | 7.325 | 31.970 |
| Cobertura SUS de UTI | **41,94%** | 47,07% | 50,13% |
| UTI sobre leitos | 17,59% | 14,20% | 12,26% |

### 🚦 Sinais para gestão

| Sinal | Evidência encontrada |
| --- | --- |
| 🔻 Cobertura SUS | Santos apresenta cobertura de leitos e UTI abaixo das referências estadual e nacional. |
| 🏢 Concentração | HHI de **1.269**; aproximadamente oito hospitais concentram 80% dos leitos. |
| 🛏️ Gap de acesso | Dez estabelecimentos possuem leitos existentes e nenhum leito SUS. |
| 🫀 Alta complexidade | Cinco estabelecimentos possuem UTI instalada e nenhuma UTI SUS. |
| 🎯 Simulação | Seriam necessários **281 leitos SUS** para igualar SP e **500** para igualar o Brasil. |

> [!IMPORTANT]
> Os resultados representam capacidade cadastrada. Eles não medem ocupação, produção hospitalar, tempo de permanência ou demanda reprimida.

<a id="arquivos"></a>
## 🗂️ Estrutura do repositório

| Arquivo | Papel no projeto |
| --- | --- |
| [`analise.ipynb`](analise.ipynb) | Notebook com preparação, validação, análise e visualizações. |
| [`hospitais CNES.xlsx`](hospitais%20CNES.xlsx) | Base local em Excel, com as abas `Leitos_2026` e `hospitais CNES`. |

## 🧰 Requisitos

- Python 3.10 ou superior.
- Jupyter Notebook.
- Pandas, NumPy, Matplotlib, Seaborn e OpenPyXL.
- A planilha `hospitais CNES.xlsx` deve permanecer na raiz do projeto.

<a id="execucao"></a>
## 🚀 Execução

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

Abra o notebook no navegador, execute as células na ordem e mantenha o arquivo Excel no mesmo diretório do notebook.

<details>
<summary><strong>⚠️ Ajuste necessário para executar o notebook salvo</strong></summary>

O notebook atualmente referencia `df_atual`, `df_santos` e `df_santos_atual` antes de definir esses recortes. Depois da célula de normalização de texto, insira temporariamente o bloco abaixo ou adicione uma célula equivalente ao notebook:

```python
df_atual = df[df["COMP"] == df["COMP"].max()].copy()
df_santos = df[df["MUNICIPIO_NORM"] == "SANTOS"].copy()
df_santos_atual = df_atual[df_atual["MUNICIPIO_NORM"] == "SANTOS"].copy()
```

</details>

<a id="metodologia"></a>
## 🧪 Metodologia

```text
Excel → validação → normalização → recortes → indicadores → comparações → recomendações
```

1. Carrega a aba `Leitos_2026` da planilha.
2. Verifica nulos, valores negativos, zeros e duplicidades nas colunas numéricas.
3. Normaliza nomes de municípios, bairros e unidades para reduzir problemas de acentuação.
4. Usa a maior competência disponível como fotografia atual da rede.
5. Agrega leitos e UTI por município, hospital e bairro.
6. Compara Santos com São Paulo e Brasil.
7. Calcula concentração da oferta por HHI e participação acumulada.
8. Simula o volume de leitos SUS necessário para alcançar referências estadual e nacional.

| Métrica | Fórmula |
| --- | --- |
| Cobertura SUS de leitos | `LEITOS_SUS / LEITOS_EXISTENTES` |
| Cobertura SUS de UTI | `UTI_TOTAL_SUS / UTI_TOTAL_EXIST` |
| UTI sobre leitos | `UTI_TOTAL_EXIST / LEITOS_EXISTENTES` |
| HHI de leitos | soma dos quadrados das participações percentuais por hospital |

## 📈 Saídas analíticas

O notebook gera painéis e tabelas para:

- evolução mensal de leitos e UTI em Santos;
- comparação entre Santos, São Paulo e Brasil;
- ranking de municípios paulistas por leitos existentes;
- análise individual dos hospitais de Santos;
- concentração da oferta e curva de Pareto;
- perfil de UTI por subtipo;
- distribuição territorial por bairro;
- gap de leitos e UTI não SUS;
- matriz de risco por porte hospitalar e cobertura SUS;
- variação entre competências e auditoria de dados cadastrais.

<a id="limitacoes"></a>
## ⚠️ Limitações conhecidas

- A base contém apenas as competências `202601`, `202602` e `202603`; a série ainda não representa uma tendência histórica longa.
- Os indicadores medem capacidade cadastrada, não ocupação, produção hospitalar, tempo de permanência ou demanda reprimida.
- O notebook contém uma célula com `NameError` por falta das definições dos recortes `df_atual`, `df_santos` e `df_santos_atual`.
- A planilha inclui campos de contato, como `NU_TELEFONE` e `NO_EMAIL`; revise os dados antes de publicar ou compartilhar o arquivo.
- O repositório não contém script de download, dicionário de dados ou metadados de atualização da base.

## 🛣️ Próximos passos

| Prioridade | Evolução sugerida |
| --- | --- |
| 01 | Corrigir o fluxo de preparação do notebook e adicionar um arquivo de dependências reproduzível. |
| 02 | Documentar origem, data de extração e dicionário de dados da planilha. |
| 03 | Integrar população por faixa etária para calcular leitos por 1.000 habitantes. |
| 04 | Incorporar uma série histórica de 12 meses ou mais. |
| 05 | Cruzar capacidade com internações, permanência e ocupação. |

## 📄 Licença

Nenhuma licença foi definida no repositório atual. Consulte os responsáveis antes de redistribuir o código, o notebook ou a base de dados.

<p align="center">
  <sub>Projeto de análise exploratória para apoiar decisões baseadas em evidências na saúde pública.</sub>
</p>
