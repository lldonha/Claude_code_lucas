---
name: data-analysis
description: Skill para análise de dados, criação de visualizações e geração de insights de negócio
---

# Data Analysis

Esta skill fornece frameworks e técnicas para análise de dados e geração de insights.

## Quando Usar

- Analisar datasets e arquivos CSV/Excel
- Criar visualizações de dados
- Calcular métricas e KPIs
- Identificar tendências e padrões
- Gerar relatórios analíticos

## Framework de Análise

### 1. Definir Objetivo
- Qual pergunta queremos responder?
- Quais métricas são relevantes?
- Quem é o público do resultado?

### 2. Coletar Dados
- Identificar fontes de dados
- Verificar qualidade e completude
- Documentar limitações

### 3. Explorar (EDA)
```python
# Estatísticas básicas
df.describe()
df.info()
df.isnull().sum()

# Distribuições
df['coluna'].value_counts()
df['coluna'].hist()

# Correlações
df.corr()
```

### 4. Limpar e Transformar
```python
# Remover duplicatas
df.drop_duplicates()

# Tratar nulos
df.fillna(0)
df.dropna()

# Converter tipos
df['data'] = pd.to_datetime(df['data'])
df['valor'] = df['valor'].astype(float)
```

### 5. Analisar
- Agregações e agrupamentos
- Comparações temporais
- Segmentações

### 6. Visualizar
- Escolher gráfico adequado
- Manter simplicidade
- Destacar insights

### 7. Comunicar
- Resumir principais descobertas
- Recomendar ações
- Documentar metodologia

## Tipos de Análise

### Descritiva
*O que aconteceu?*
- Médias, medianas, desvios
- Frequências e proporções
- Tendências históricas

### Diagnóstica
*Por que aconteceu?*
- Correlações
- Análise de causa raiz
- Segmentações comparativas

### Preditiva
*O que pode acontecer?*
- Projeções e forecasts
- Identificação de padrões
- Cenários

### Prescritiva
*O que fazer?*
- Recomendações baseadas em dados
- Otimização
- Priorização

## Gráficos por Tipo de Dado

| Objetivo | Gráfico | Quando Usar |
|----------|---------|-------------|
| Tendência | Linha | Dados temporais |
| Comparação | Barras | Categorias |
| Proporção | Pizza/Donut | Partes do todo |
| Distribuição | Histograma | Frequências |
| Relação | Scatter | 2 variáveis |
| Composição | Área empilhada | Mudança ao longo do tempo |

## Código para Visualização

### Gráfico de Linha (Chart.js)
```javascript
new Chart(ctx, {
  type: 'line',
  data: {
    labels: ['Jan', 'Fev', 'Mar'],
    datasets: [{
      label: 'Vendas',
      data: [100, 150, 200],
      borderColor: '#2563eb',
      tension: 0.1
    }]
  }
});
```

### Gráfico de Barras (Chart.js)
```javascript
new Chart(ctx, {
  type: 'bar',
  data: {
    labels: ['A', 'B', 'C'],
    datasets: [{
      label: 'Valores',
      data: [30, 50, 20],
      backgroundColor: ['#2563eb', '#16a34a', '#ca8a04']
    }]
  }
});
```

## Métricas Comuns

### Financeiras
- **Receita** = Σ vendas
- **Margem** = (Receita - Custo) / Receita
- **ROI** = (Ganho - Investimento) / Investimento
- **CAC** = Custo Marketing / Novos Clientes
- **LTV** = Ticket Médio × Frequência × Tempo

### Operacionais
- **Taxa de Conversão** = Conversões / Visitantes
- **Churn** = Clientes Perdidos / Total Clientes
- **NPS** = % Promotores - % Detratores
- **Tempo Médio** = Σ Tempos / N

### Crescimento
- **MoM** = (Atual - Anterior) / Anterior
- **YoY** = (Ano Atual - Ano Anterior) / Ano Anterior
- **CAGR** = (Final / Inicial)^(1/anos) - 1

## Template de Relatório Analítico

```markdown
# Análise: [Título]

## Sumário Executivo
[3-5 bullets com principais descobertas]

## Contexto
- Período: [datas]
- Fonte: [origem dos dados]
- Amostra: [tamanho]

## Metodologia
[Como foi feita a análise]

## Resultados

### KPIs Principais
| Métrica | Valor | Variação |
|---------|-------|----------|

### Análise Detalhada
[Gráficos e interpretações]

## Insights
1. [Insight 1]
2. [Insight 2]

## Recomendações
1. [Ação 1]
2. [Ação 2]

## Limitações
[Ressalvas da análise]
```

## Exemplos de Uso

```
"Use a skill data-analysis para analisar o arquivo vendas.csv e identificar tendências"

"Calcule os principais KPIs de marketing do último trimestre"

"Crie uma visualização comparando performance entre regiões"
```
