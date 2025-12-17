---
name: document-creation
description: Skill para criar documentos profissionais formatados em Markdown, HTML e outros formatos
---

# Document Creation

Esta skill fornece templates e orientações para criar documentos profissionais bem formatados.

## Quando Usar

- Criar relatórios executivos
- Elaborar propostas comerciais
- Gerar documentação técnica
- Formatar apresentações em Markdown
- Criar emails profissionais

## Estrutura de Documentos

### Relatório Executivo
```markdown
# [Título do Relatório]

**Data:** [data]
**Autor:** [nome]
**Versão:** [versão]

---

## Sumário Executivo
[Resumo de 2-3 parágrafos com principais conclusões]

## Contexto
[Background e motivação]

## Metodologia
[Como foi feito]

## Resultados
### [Resultado 1]
### [Resultado 2]

## Conclusões
[Principais takeaways]

## Recomendações
1. [Recomendação 1]
2. [Recomendação 2]

## Próximos Passos
- [ ] Ação 1
- [ ] Ação 2

---
*Documento gerado em [data]*
```

### Proposta Comercial
```markdown
# Proposta Comercial

**Para:** [Cliente]
**De:** [Empresa]
**Data:** [data]
**Validade:** [dias] dias

---

## 1. Apresentação
[Breve apresentação da empresa]

## 2. Entendimento da Necessidade
[O que o cliente precisa]

## 3. Solução Proposta
[Detalhamento da solução]

## 4. Escopo
### Incluído
- Item 1
- Item 2

### Não Incluído
- Item 1

## 5. Cronograma
| Fase | Descrição | Prazo |
|------|-----------|-------|
| 1    |           |       |

## 6. Investimento
| Item | Valor |
|------|-------|
| Total | R$ |

## 7. Condições
[Forma de pagamento, garantias]

## 8. Aceite
[Espaço para assinatura]
```

### Ata de Reunião
```markdown
# Ata de Reunião

**Data:** [data]
**Horário:** [início] - [fim]
**Local:** [local/link]

## Participantes
- [Nome] - [Função]

## Pauta
1. [Item 1]
2. [Item 2]

## Discussões
### [Tópico 1]
[Resumo da discussão]

### [Tópico 2]
[Resumo da discussão]

## Decisões
1. [Decisão 1]
2. [Decisão 2]

## Ações
| Ação | Responsável | Prazo |
|------|-------------|-------|
|      |             |       |

## Próxima Reunião
**Data:** [data]
**Pauta prévia:** [itens]

---
*Ata elaborada por [nome]*
```

## Formatação HTML

### Dashboard Template
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    :root {
      --primary: #2563eb;
      --success: #16a34a;
      --bg: #f8fafc;
    }
    body { font-family: system-ui; background: var(--bg); }
    .container { max-width: 1200px; margin: 0 auto; padding: 2rem; }
    .card { background: white; border-radius: 8px; padding: 1.5rem; box-shadow: 0 1px 3px rgba(0,0,0,0.1); }
    .kpi { text-align: center; }
    .kpi-value { font-size: 2rem; font-weight: bold; color: var(--primary); }
    .kpi-label { color: #6b7280; font-size: 0.875rem; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Dashboard</h1>
    <div class="grid">
      <div class="card kpi">
        <div class="kpi-value">R$ 0</div>
        <div class="kpi-label">Receita</div>
      </div>
    </div>
  </div>
</body>
</html>
```

## Convenções de Estilo

### Títulos
- H1: Título principal (1 por documento)
- H2: Seções principais
- H3: Subseções
- H4: Detalhamentos

### Listas
- Bullets para itens sem ordem
- Números para sequências/passos
- Checkboxes para tarefas

### Tabelas
- Cabeçalho em negrito
- Alinhamento consistente
- Células concisas

### Destaques
- **Negrito** para ênfase
- *Itálico* para termos técnicos
- `Código` para comandos/variáveis
- > Citações para notas importantes

## Exemplos de Uso

```
"Use a skill document-creation para criar um relatório executivo sobre o projeto X"

"Gere uma proposta comercial para o cliente Y usando o template padrão"

"Formate este conteúdo como uma ata de reunião profissional"
```
