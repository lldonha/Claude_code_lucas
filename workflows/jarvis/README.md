# JARVIS Workflows

Workflows n8n do assistente JARVIS.

## Workflows Disponiveis

### 1. JARVIS v3 - Dual Interface + Vision
**ID:** `xSjW1LDJxZPMAqrU`
**Arquivo:** `jarvis-v3-dual-interface.json`
**Versao:** 3.1.0

Assistente inteligente com suporte a Telegram e Chat n8n nativo.

**Funcionalidades:**
- 📱 Telegram Trigger (texto, audio, imagem)
- 💬 Chat n8n nativo
- 🎙️ Transcricao de audio com Gemini 2.0 Flash
- 👁️ Analise de imagem com Gemini 2.5 Pro (Vision)
- 🤖 AI Agent com Claude Code SSH Tool v2
- 🧠 Memoria PostgreSQL persistente
- 🔀 Roteamento automatico de resposta
- 📌 Sticky notes com documentacao inline

**Error Workflow:** JARVIS Monitor v1.3 (`3wYi0Am7KUn5j3xV`)

**URL:** https://n8n.lldonha.com/workflow/xSjW1LDJxZPMAqrU

---

### 2. JARVIS Monitor v1.3
**ID:** `3wYi0Am7KUn5j3xV`
**Arquivo:** `jarvis-monitor-v1.3.json`
**Versao:** 1.3.0

Monitor inteligente do JARVIS v3 com auto-correcao, relatorios e backup no GitHub.

**Funcionalidades:**
- 🚨 Error Trigger instantaneo (captura erros em tempo real)
- ⚙️ Classificacao automatica de erros (TIMEOUT, RATE_LIMIT, CONNECTION, AUTH, PERMISSION, VALIDATION)
- 🔄 Auto-correcao para erros corrigiveis via Claude Code
- 💾 Backup automatico antes de qualquer correcao
- 📊 Relatorio diario as 9h com limpeza de registros >30 dias
- 📅 Backup semanal no GitHub (domingo 10h)
- 📱 Notificacao via Telegram
- 🗄️ Persistencia PostgreSQL (jarvis_executions)

**Classificacao de Erros:**
- **Corrigivel:** TIMEOUT, RATE_LIMIT, CONNECTION
- **Nao Corrigivel:** AUTH, PERMISSION, VALIDATION, UNKNOWN

**URL:** https://n8n.lldonha.com/workflow/3wYi0Am7KUn5j3xV

---

### 3. Claude Code SSH Tool v2
**ID:** `PAHq9uOzVd8l9ybX`
**Arquivo:** `claude-code-ssh-tool-v2.json`
**Versao:** 2.0.0
**Tipo:** Sub-workflow (Tool)

Executa comandos no Claude Code CLI via SSH.

**Input:**
- `query` ou `prompt`: Comando/pergunta para o Claude Code
- `session_id` (opcional): UUID da sessao

**Output:**
- `success`: boolean
- `response`: texto da resposta
- `error`: mensagem de erro (se houver)
- `exit_code`: codigo de saida do comando

**Chamado por:**
- JARVIS v3 (`xSjW1LDJxZPMAqrU`)
- JARVIS Monitor v1.3 (`3wYi0Am7KUn5j3xV`)

**URL:** https://n8n.lldonha.com/workflow/PAHq9uOzVd8l9ybX

---

## Arquitetura

```
┌─────────────────────────────────────────────────────────────┐
│                 🤖 JARVIS v3 (xSjW1LDJxZPMAqrU)              │
│                                                              │
│  📱 Telegram ─┐                                              │
│    - Texto    │                                              │
│    - Audio    ├──→ Processar ──→ AI Agent ──→ Responder     │
│    - Imagem   │         │                                    │
│  💬 Chat n8n ─┘         ↓                                    │
│                  Claude Code SSH Tool v2                     │
│                  (PAHq9uOzVd8l9ybX)                          │
│                         ↓                                    │
│            Acesso ao Sistema (n8n, arquivos, etc)           │
└─────────────────────────────────────────────────────────────┘
                         │
          ┌──────────────┼──────────────┐
          │         Error Trigger       │
          │    (captura instantanea)    │
          ↓                             ↓
┌─────────────────────────────────────────────────────────────┐
│              🔧 JARVIS Monitor v1.3 (3wYi0Am7KUn5j3xV)       │
│                                                              │
│  🚨 Error Trigger ─→ Classificar ─→ Corrigivel?             │
│                            │             │                   │
│                            ↓            SIM                  │
│                      NAO: Notifica       ↓                   │
│                                    Backup + Corrigir         │
│                                                              │
│  📊 Schedule (9h)    ─→ Relatorio Diario + Limpeza 30d      │
│  📅 Schedule (dom 10h) ─→ Relatorio Semanal + GitHub Backup │
│                           ↓                                  │
│                      PostgreSQL                              │
│                  (jarvis_executions)                         │
└─────────────────────────────────────────────────────────────┘
                         ↓
                    Backup Semanal
                         ↓
┌─────────────────────────────────────────────────────────────┐
│           📦 GitHub (lldonha/Claude_code_lucas)              │
│  - Branch: backup-YYYY-MM-DD                                 │
│  - workflows/jarvis/backups/                                 │
│  - workflows/jarvis/reports/                                 │
└─────────────────────────────────────────────────────────────┘
```

## Fluxo de Auto-Correcao

```
Erro Detectado
      ↓
┌─────────────┐
│ Classificar │
│    Erro     │
└─────────────┘
      ↓
┌─────────────────────────────────────┐
│ TIMEOUT / RATE_LIMIT / CONNECTION?  │
└─────────────────────────────────────┘
      │                    │
     SIM                  NAO
      ↓                    ↓
┌───────────┐      ┌────────────────┐
│  Backup   │      │   Notificar    │
│ Workflow  │      │   Telegram     │
└───────────┘      │ (nao corrigir) │
      ↓            └────────────────┘
┌───────────┐
│ Claude    │
│ Corrige   │
└───────────┘
      ↓
┌───────────┐
│ Notificar │
│ Correcao  │
└───────────┘
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
| 🚨 Error Trigger | Instantaneo | Captura erros em tempo real |
| 📊 Relatorio Diario | 09:00 | Resumo 24h + limpeza >30 dias |
| 📅 Backup Semanal | Domingo 10:00 | Relatorio 7 dias + backup GitHub |

## Versoes

### JARVIS v3
- **v3.1.0** - 18/12/2025
  - Sticky notes com documentacao inline
  - Emojis em todos os nodes
  - Error Workflow apontando para Monitor v1.3
  - Sub-workflow documentado
- **v3.0.0** - 17/12/2025
  - Dual Interface (Telegram + Chat)
  - Vision (analise de imagens)
  - Audio transcription
  - PostgreSQL memory
  - Error handling

### JARVIS Monitor
- **v1.3.0** - 18/12/2025
  - Error Trigger instantaneo (substitui polling 5min)
  - Classificacao automatica de erros
  - Logica de auto-correcao (backup + corrigir)
  - Sticky notes com documentacao inline
- **v1.1.0** - 17/12/2025
  - Backup semanal no GitHub
  - Persistencia PostgreSQL
  - Relatorio semanal detalhado
  - Limpeza automatica >30 dias
- **v1.0.0** - 17/12/2025
  - Monitoramento de erros
  - Analise com Claude Code
  - Relatorio diario

### Claude Code SSH Tool
- **v2.0.0** - 18/12/2025
  - Sticky note com documentacao
  - Emojis nos nodes
  - Input/Output documentado
  - Chamado por JARVIS v3 e Monitor

---

## Estrutura de Backups

O backup semanal cria automaticamente:
- Nova branch: `backup-YYYY-MM-DD`
- Arquivo: `workflows/jarvis/backups/jarvis-v3-YYYY-MM-DD.json`
- Relatorio: `workflows/jarvis/reports/weekly-YYYY-MM-DD.md`

---

*Workspace JARVIS - Lucas (lldonha)*
*Dezembro 2025*
