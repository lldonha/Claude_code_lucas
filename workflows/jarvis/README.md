# JARVIS v3 - Dual Interface + Vision

Assistente inteligente com suporte a Telegram e Chat n8n nativo.

## Funcionalidades

- **Telegram Trigger**: Recebe texto, audio e imagens
- **Chat n8n nativo**: Interface de chat integrada
- **Transcricao de Audio**: Gemini 2.0 Flash
- **Analise de Imagem**: Gemini 2.5 Pro (Vision)
- **AI Agent**: Com Claude Code SSH Tool
- **Memoria**: PostgreSQL persistente por sessao
- **Roteamento Automatico**: Entrada define saida

## Arquitetura

```
Telegram/Chat --> Detectar Tipo --> Processar --> AI Agent --> Responder
                       |                             |
                  Audio? Imagem?              Claude Code SSH
                       |                             |
                  Gemini API                 Acesso ao Sistema
```

## Fluxo de Dados

1. **Entrada**: Telegram ou Chat trigger
2. **Deteccao**: Verifica se e audio, imagem ou texto
3. **Processamento**:
   - Audio: Transcricao via Gemini
   - Imagem: Analise via Gemini Vision
   - Texto: Direto
4. **AI Agent**: Processa com memoria e ferramentas
5. **Saida**: Roteia para origem (Telegram/Chat)

## Dependencias

### Credenciais Necessarias
- `telegramApi`: Bot do Telegram (TEST)
- `googlePalmApi`: API do Google Gemini (LLDONHA)
- `postgres`: Banco PostgreSQL (Jarvis)

### Workflows Auxiliares
- `t4Mv1Ko6FptZs4fK`: Claude Code SSH Tool
- `1FRDFNWj1QfDqWfH`: Error Workflow

### PostgreSQL
- Database: `jarvis_db`
- Tabela: `jarvis_chat_history`

## Configuracao

1. Configure as credenciais no n8n
2. Ajuste o bot do Telegram
3. Configure o PostgreSQL
4. Ative o workflow

## Arquivos

- `jarvis-v3-dual-interface.json` - Workflow completo para importar no n8n

## URL de Producao

https://n8n.lldonha.com/workflow/xSjW1LDJxZPMAqrU

## Versao

- **v3.0.0** - 17/12/2025
  - Dual Interface (Telegram + Chat)
  - Vision (analise de imagens)
  - Audio transcription
  - PostgreSQL memory
  - Error handling com roteamento
