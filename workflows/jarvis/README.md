# JARVIS Workflows

Workflows n8n do assistente JARVIS.

## Workflows Disponiveis

### 1. JARVIS v3 - Dual Interface + Vision
**ID:** `xSjW1LDJxZPMAqrU`
**Arquivo:** `jarvis-v3-dual-interface.json`

Assistente inteligente com suporte a Telegram e Chat n8n nativo.

**Funcionalidades:**
- Telegram Trigger (texto, audio, imagem)
- Chat n8n nativo
- Transcricao de audio com Gemini 2.0 Flash
- Analise de imagem com Gemini 2.5 Pro (Vision)
- AI Agent com Claude Code SSH Tool
- Memoria PostgreSQL persistente
- Roteamento automatico de resposta

**URL:** https://n8n.lldonha.com/workflow/xSjW1LDJxZPMAqrU

---

### 2. JARVIS Monitor v1
**ID:** `3wYi0Am7KUn5j3xV`
**Arquivo:** `jarvis-monitor-v1.json`

Monitoramento automatico do JARVIS v3 com analise inteligente.

**Funcionalidades:**
- Monitoramento de erros a cada 5 minutos
- Analise automatica com Claude Code SSH Tool
- Decisao inteligente: corrigir ou notificar
- Notificacao via Telegram
- Relatorio diario as 9h

**URL:** https://n8n.lldonha.com/workflow/3wYi0Am7KUn5j3xV

---

## Arquitetura

```
┌─────────────────────────────────────────────────────────────┐
│                      JARVIS v3                               │
│  Telegram/Chat → Processar → AI Agent → Responder           │
│                      ↓                                       │
│              Claude Code SSH Tool                            │
│                      ↓                                       │
│            Acesso ao Sistema (n8n, arquivos, etc)           │
└─────────────────────────────────────────────────────────────┘
                         ↑
                    Monitorado por
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                   JARVIS Monitor v1                          │
│  Schedule (5min) → Claude Code → Analise → Telegram         │
│  Schedule (9h)   → Claude Code → Relatorio → Telegram       │
└─────────────────────────────────────────────────────────────┘
```

## Dependencias

### Credenciais Necessarias
- `telegramApi`: Bot do Telegram
- `googlePalmApi`: API do Google Gemini
- `postgres`: Banco PostgreSQL

### Workflows Auxiliares
- `PAHq9uOzVd8l9ybX`: Claude Code SSH Tool v2
- `t4Mv1Ko6FptZs4fK`: Claude Code SSH Tool (original)
- `1FRDFNWj1QfDqWfH`: Error Workflow

### PostgreSQL
- Database: `jarvis_db`
- Tabela: `jarvis_chat_history`

## Configuracao

1. Importe os workflows no n8n
2. Configure as credenciais
3. Ajuste os IDs de workflow nos nodes
4. Ative os workflows

## Versoes

### JARVIS v3
- **v3.0.0** - 17/12/2025
  - Dual Interface (Telegram + Chat)
  - Vision (analise de imagens)
  - Audio transcription
  - PostgreSQL memory
  - Error handling

### JARVIS Monitor v1
- **v1.0.0** - 17/12/2025
  - Monitoramento de erros
  - Analise com Claude Code
  - Relatorio diario
