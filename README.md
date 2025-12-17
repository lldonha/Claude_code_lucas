# JARVIS - Claude Code Workspace

Workspace pessoal do Claude Code com agentes especializados, skills reutilizáveis e integrações MCP.

## Estrutura

```
Claude_code_lucas/
├── CLAUDE.md                    # System prompt + roteamento
├── .claude-plugin/              # Configuração de plugin
│   └── manifest.json
├── agents/                      # Agentes especializados
│   ├── perito-tecnico/          # Laudos e documentação técnica
│   ├── assistente-pessoal/      # Calendário e produtividade
│   ├── analista-dados/          # Análises e dashboards
│   └── social-media/            # Conteúdo e redes sociais
├── skills/                      # Skills reutilizáveis
│   ├── pericias/                # Templates de perícias
│   ├── n8n-automation/          # Padrões de automação
│   ├── document-creation/       # Criação de documentos
│   └── data-analysis/           # Análise de dados
├── context/                     # Arquivos de contexto
│   ├── business/                # Contexto de negócio
│   ├── templates/               # Templates reutilizáveis
│   └── knowledge/               # Base de conhecimento
├── workflows/                   # Workflows n8n
└── mcp/                         # Configuração MCP
```

## Agentes Disponíveis

| Agente | Função | Triggers |
|--------|--------|----------|
| `@perito-tecnico` | Laudos, vistorias, pareceres | laudo, perícia, vistoria |
| `@assistente-pessoal` | Calendário, tarefas, emails | agenda, tarefa, lembrete |
| `@analista-dados` | Dashboards, relatórios | análise, dashboard, dados |
| `@social-media` | Posts, conteúdo | post, conteúdo, redes |

## Skills

- **pericias** - Templates ABNT para documentação técnica
- **n8n-automation** - Padrões para workflows n8n
- **document-creation** - Criação de documentos profissionais
- **data-analysis** - Frameworks de análise de dados

## Instalação como Plugin

Para instalar este workspace como plugin em outro projeto Claude Code:

```bash
# No terminal do Claude Code
/plugin marketplace add lldonha/Claude_code_lucas

# Instalar skills específicas
/plugin install pericias@lldonha-workspace
/plugin install n8n-automation@lldonha-workspace
```

## Uso

### Chamar um agente
```
@perito-tecnico crie um laudo de avaliação para o imóvel X
@analista-dados analise o arquivo vendas.csv
```

### Usar uma skill
```
Use a skill pericias para criar um parecer técnico
Aplique a skill document-creation para formatar este relatório
```

## Integrações

- **n8n**: https://n8n.lldonha.com
- **MCP Gateway**: localhost:8811
- **Telegram Bot**: JARVIS

## Autor

Lucas ([@lldonha](https://github.com/lldonha))

---

*Dezembro 2025*
