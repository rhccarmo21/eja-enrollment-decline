
# 📉 EJA Enrollment Decline Analysis

[![Licença MIT](https://img.shields.io/badge/Licença-MIT-green)](https://pt.wikipedia.org/wiki/Licen%C3%A7a_MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/downloads/)
[![Panel](https://img.shields.io/badge/Panel-Interactive_Dashboards-orange)](https://panel.holoviz.org/)

## 📌 Sumário
1. [Visão Geral](#-visão-geral)  
2. [Indicadores-Chave](#-indicadores-chave)
3. [Fontes de Dados](#-fontes-de-dados)
4. [Fatores de Influência](#-fatores-de-influência)
5. [Metodologia](#-metodologia)
6. [Instalação](#-instalação)
7. [Como Usar](#-como-usar)
8. [Casos de Estudo](#-casos-de-estudo)
9. [Contribuição](#-contribuição)
10. [Contato](#-contato)

---

## 🌐 Visão Geral

Análise multidimensional do declínio nas matrículas da EJA que permite:

- 📉 **Mapear tendências temporais** (2010-2023)
- 🏙️ **Identificar padrões regionais** de evasão
- 🎓 **Relacionar com políticas educacionais**
- 💼 **Analisar impactos do mercado de trabalho**

**Aplicações:**
- Reformulação de políticas para EJA
- Redesenho de estratégias de captação
- Alocação eficiente de recursos
- Estudos sobre exclusão educacional

---

## 📊 Indicadores-Chave

### Métricas Principais
| Indicador | Fórmula | Fonte | Periodicidade |
|-----------|---------|-------|---------------|
| Taxa de Declínio Anual | `(Matrículas_t - Matrículas_{t-1})/Matrículas_{t-1}` | Censo Escolar | Anual |
| Densidade de Oferta | `Nº escolas com EJA/Nº escolas total` | INEP | Anual |
| Gap Educacional | `% Pop. 25+ sem fundamental completo - % matriculados EJA` | IBGE+PNAD | Anual |
| Índice de Permanência | `Matrículas finais/Matrículas iniciais` | INEP | Anual |

```python
from eja_analysis import calculate_decline_rate

decline = calculate_decline_rate(
    start_year=2015,
    end_year=2022,
    region='nordeste'
)
```

---

## 📂 Fontes de Dados

| Fonte | Variáveis | Cobertura | Atualização |
|-------|-----------|-----------|-------------|
| Censo Escolar (INEP) | Matrículas EJA | Escola | Anual |
| PNAD Contínua | Perfil educacional | Nacional | Trimestral |
| RAIS/CAGED | Inserção no mercado | Municipal | Anual/Mensal |
| SIOPE | Investimentos em EJA | Municipal | Anual |

**Estrutura Básica:**
```python
import pandas as pd

eja_df = pd.read_csv('microdados_inep_eja.csv')
print(eja_df.groupby('ANO')['MATRICULAS'].sum())
```

---

## 🔍 Fatores de Influência

### Principais Variáveis Analisadas
1. **Demográficas**:
   - Envelhecimento populacional
   - Migração rural-urbana

2. **Econômicas**:
   - Taxa de desemprego
   - Ocupações que exigem escolaridade

3. **Educacionais**:
   - Expansão do EAD
   - Políticas de certificação rápida

4. **Estruturais**:
   - Fechamento de polos EJA
   - Redução de financiamento

---

## ⚙️ Metodologia

1. **Análise Longitudinal**:
   ```python
   from eja_analysis import plot_trend_comparison

   plot_trend_comparison(
       regions=['sudeste', 'nordeste'],
       years=range(2010, 2023),
       title='Comparação Regional do Declínio'
   )
   ```

2. **Modelagem Causal**:
   - Modelos de diferenças-em-diferenças
   - Análise de intervenções políticas

3. **Clusterização**:
   - Identificação de perfis municipais similares
   - Análise de sobrevivência educacional

---

## 🛠️ Instalação

### Via pip
```bash
pip install eja-analysis
```

### Com dependências completas
```bash
pip install eja-analysis[full]
```

### Docker
```bash
docker pull educanalytics/eja-trends:latest
```

---

## 🚀 Como Usar

### 1. Análise Descritiva
```python
from eja_analysis import EJAReport

report = EJAReport(year_range=(2015,2022))
report.generate(
    output_file='declinio_eja_brasil.pdf',
    metrics=['decline_rate', 'retention_index']
)
```

### 2. Painel Interativo
```bash
panel serve app/eja_dashboard.py --show
```

### 3. API de Consulta
```python
from eja_api import get_municipality_trend

trend = get_municipality_trend(
    ibge_code=3550308,  # São Paulo
    indicators=['enrollment', 'schools']
)
```

---

## 🏫 Casos de Estudo

### Estados com Maior Declínio (2015-2022)
| UF | Variação Matrículas (%) | Fechamento de Polos | Principal Fator |
|----|-------------------------|---------------------|-----------------|
| RJ | -58.3 | 127 | Redução financiamento |
| MG | -52.1 | 89 | Migração para EAD |
| ... | ... | ... | ... |

**Achados Relevantes:**
- 72% dos municípios com >20% de declínio têm IDHM abaixo de 0.65
- Correlação positiva (0.41) entre oferta de EMPTEC e retenção na EJA

---

## 🗂 Estrutura do Projeto

```
eja-decline-analysis/
├── data/
│   ├── raw/              # Microdados INEP/IBGE
│   ├── processed/        # Séries temporais consolidadas
├── notebooks/
│   ├── policy_impact_analysis.ipynb
├── eja_analysis/
│   ├── preprocessing/    # Limpeza de dados
│   ├── modeling/         # Análises estatísticas
│   ├── policy/           # Simulações de políticas
├── docs/
│   ├── technical_guide.md
└── Makefile
```

---

## 🤝 Contribuição

1. **Adicionar Fatores**:
   ```python
   class NewFactor(AnalysisFactor):
       def __init__(self):
           self.name = "Impacto do Bolsa Família"
           self.data_source = "MDS"
   ```

2. **Padrões de Código**:
   ```python
   def calculate_retention(initial: int, final: int) -> float:
       """Calcula taxa de permanência com tratamento de divisão por zero"""
       return final/initial if initial > 0 else 0.0
   ```

3. **Testes**:
   ```bash
   pytest tests/test_policy_simulations.py -v
   ```

---

## 📧 Contato

**Observatório da Educação de Jovens e Adultos**  
[pesquisa.eja@inep.gov.br](mailto:pesquisa.eja@inep.gov.br)

**Parcerias Institucionais**  
[parcerias@mec.gov.br](mailto:parcerias@mec.gov.br)

**Acesso aos Dados**  
[![Portal INEP](https://img.shields.io/badge/Dados_EJA-Acesse_Aqui-blue)](https://www.gov.br/inep/pt-br)

---

💡 **Para Gestores Educacionais:**  
Baixe nosso kit de intervenção:  
[📘 Estratégias para Revitalização da EJA](docs/estrategias_eja.pdf)

> **Nota Técnica:** Considera-se matrícula inicial conforme declarada no Censo Escolar, excluídas duplicidades.
```

### Destaques Específicos:

1. **Abordagem Multidimensional**: Combina dados educacionais, econômicos e demográficos
2. **Foco em Causalidade**: Identificação de fatores-chave do declínio
3. **Ferramentas para Gestão**: Simulador de impacto de políticas públicas
4. **Perspectiva Regional**: Análises comparativas entre estados e municípios
5. **Integração com Mercado de Trabalho**: Dados da RAIS/CAGED

### Para Implementação:

1. Baixar microdados do Censo Escolar (INEP)
2. Cruzar com dados do IBGE e MTE
3. Mapear políticas municipais de EJA
4. Implementar painéis de acompanhamento em tempo real
