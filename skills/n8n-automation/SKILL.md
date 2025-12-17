---
name: n8n-automation
description: Skill para criar, gerenciar e otimizar workflows de automação no n8n
---

# n8n Automation

Esta skill fornece conhecimento e padrões para criar workflows eficientes no n8n.

## Quando Usar

- Criar novos workflows de automação
- Otimizar workflows existentes
- Debugar erros em automações
- Integrar serviços via API
- Configurar triggers e webhooks

## Estrutura de Workflow

### Padrão Básico
```
[Trigger] → [Processar] → [Ação] → [Notificar]
```

### Com Tratamento de Erro
```
[Trigger] → [Try] → [Processar] → [Ação]
              ↓
          [Catch] → [Log Erro] → [Notificar]
```

### Com Roteamento
```
[Trigger] → [Switch] → [Rota A] → [Ação A]
                   ↘ [Rota B] → [Ação B]
                   ↘ [Default] → [Fallback]
```

## Nodes Comuns

### Triggers
- **Webhook** - Receber requisições HTTP
- **Schedule** - Execução agendada (cron)
- **Telegram Trigger** - Mensagens do Telegram
- **Email Trigger (IMAP)** - Novos emails

### Processamento
- **Code** - JavaScript/Python customizado
- **Set** - Definir variáveis
- **IF** - Condicionais
- **Switch** - Múltiplas rotas
- **Merge** - Combinar dados

### Integrações
- **HTTP Request** - Chamadas API
- **Postgres** - Banco de dados
- **Google Sheets** - Planilhas
- **Telegram** - Mensagens

## Padrões de Código

### Acessar Dados do Trigger
```javascript
// Webhook data
const body = $input.first().json;
const message = body.message;

// Telegram message
const chatId = $('Telegram Trigger').first().json.message.chat.id;
const text = $('Telegram Trigger').first().json.message.text;
```

### Formatar Resposta
```javascript
return {
  json: {
    success: true,
    data: processedData,
    timestamp: new Date().toISOString()
  }
};
```

### Tratamento de Erro
```javascript
try {
  // Lógica principal
  const result = await processData(input);
  return { json: { success: true, result } };
} catch (error) {
  return { json: { success: false, error: error.message } };
}
```

## Templates de Workflow

### Telegram Bot Básico
```json
{
  "nodes": [
    {"type": "n8n-nodes-base.telegramTrigger"},
    {"type": "n8n-nodes-base.code", "name": "Processar"},
    {"type": "n8n-nodes-base.telegram", "name": "Responder"}
  ]
}
```

### Webhook + Database
```json
{
  "nodes": [
    {"type": "n8n-nodes-base.webhook"},
    {"type": "n8n-nodes-base.postgres", "name": "Query"},
    {"type": "n8n-nodes-base.respondToWebhook"}
  ]
}
```

### Scheduled Report
```json
{
  "nodes": [
    {"type": "n8n-nodes-base.scheduleTrigger"},
    {"type": "n8n-nodes-base.postgres", "name": "Fetch Data"},
    {"type": "n8n-nodes-base.code", "name": "Format"},
    {"type": "n8n-nodes-base.telegram", "name": "Send Report"}
  ]
}
```

## Boas Práticas

1. **Nomeie nodes claramente** - Descreva a função
2. **Use Error Workflow** - Configure tratamento global
3. **Valide inputs** - Verifique dados de entrada
4. **Log importante** - Registre ações críticas
5. **Timeout adequado** - Configure limites de tempo
6. **Credenciais seguras** - Use variáveis de ambiente

## Debugging

### Verificar Execução
```javascript
console.log('Input:', JSON.stringify($input.all(), null, 2));
console.log('Item:', $input.first().json);
```

### Testar Webhook
```bash
curl -X POST https://n8n.lldonha.com/webhook/test \
  -H "Content-Type: application/json" \
  -d '{"test": "data"}'
```

## Exemplos de Uso

```
"Use a skill n8n-automation para criar um workflow que monitora emails e envia alertas no Telegram"

"Otimize o workflow de classificação de mensagens usando as melhores práticas"

"Crie um webhook que recebe dados e salva no Postgres"
```

## Referências

- Documentação n8n: https://docs.n8n.io
- n8n Community: https://community.n8n.io
- Instância local: https://n8n.lldonha.com
