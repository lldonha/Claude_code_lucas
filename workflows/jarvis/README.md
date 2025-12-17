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

### 2. JARVIS Monitor v1.1
**ID:** `3wYi0Am7KUn5j3xV`
**Arquivo:** `jarvis-monitor-v1.json`

Monitoramento automatico do JARVIS v3 com analise inteligente e backup automatico.

**Funcionalidades:**
- Monitoramento de erros a cada 5 minutos
- Analise automatica com Claude Code SSH Tool
- Persistencia no PostgreSQL (retencao de 30 dias)
- Relatorio diario as 9h com limpeza automatica
- Backup semanal no GitHub (domingo 10h)
- Notificacao via Telegram

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
│                   JARVIS Monitor v1.1                        │
│                                                              │
│  Schedule (5min)  → Claude Code → PostgreSQL → Telegram     │
│  Schedule (9h)    → Claude Code → Limpar 30d → Telegram     │
│  Schedule (dom 10h) → Claude Code → GitHub → Telegram       │
│                           ↓                                  │
│                      PostgreSQL                              │
│                  (jarvis_executions)                         │
└─────────────────────────────────────────────────────────────┘
                         ↓
                    Backup Semanal
                         ↓
┌─────────────────────────────────────────────────────────────┐
│                GitHub (lldonha/Claude_code_lucas)            │
│  - Branch: backup-YYYY-MM-DD                                 │
│  - workflows/jarvis/backups/                                 │
│  - workflows/jarvis/reports/                                 │
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
- Tabelas:
  - `jarvis_chat_history` - Memoria do chat
  - `jarvis_executions` - Historico de execucoes (30 dias)

#### Schema jarvis_executions
```sql
CREATE TABLE IF NOT EXISTS jarvis_executions (
    id SERIAL PRIMARY KEY,
    execution_id VARCHAR(50),
    workflow_id VARCHAR(50),
    workflow_name VARCHAR(100),
    status VARCHAR(20),
    started_at TIMESTAMP,
    finished_at TIMESTAMP,
    duration_ms INTEGER,
    error_message TEXT,
    error_node VARCHAR(100),
    analysis TEXT,
    action_taken VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_jarvis_exec_workflow ON jarvis_executions(workflow_id);
CREATE INDEX idx_jarvis_exec_status ON jarvis_executions(status);
CREATE INDEX idx_jarvis_exec_created ON jarvis_executions(created_at);
```

## Configuracao

1. Importe os workflows no n8n
2. Configure as credenciais
3. Crie a tabela `jarvis_executions` no PostgreSQL
4. Ajuste os IDs de workflow nos nodes
5. Ative os workflows

## Agendamentos

| Trigger | Horario | Funcao |
|---------|---------|--------|
| Verificar Erros | A cada 5 min | Monitora erros e analisa correcoes |
| Relatorio Diario | 09:00 | Resumo 24h + limpeza >30 dias |
| Backup Semanal | Domingo 10:00 | Relatorio 7 dias + backup GitHub |

## Versoes

### JARVIS v3
- **v3.0.0** - 17/12/2025
  - Dual Interface (Telegram + Chat)
  - Vision (analise de imagens)
  - Audio transcription
  - PostgreSQL memory
  - Error handling

### JARVIS Monitor v1
- **v1.1.0** - 17/12/2025
  - Backup semanal no GitHub
  - Persistencia PostgreSQL
  - Relatorio semanal detalhado
  - Limpeza automatica >30 dias
- **v1.0.0** - 17/12/2025
  - Monitoramento de erros
  - Analise com Claude Code
  - Relatorio diario

---

## Estrutura de Backups

O backup semanal cria automaticamente:
- Nova branch: `backup-YYYY-MM-DD`
- Arquivo: `workflows/jarvis/backups/jarvis-v3-YYYY-MM-DD.json`
- Relatorio: `workflows/jarvis/reports/weekly-YYYY-MM-DD.md`

---

*Workspace JARVIS - Lucas (lldonha)*
*Dezembro 2025*
