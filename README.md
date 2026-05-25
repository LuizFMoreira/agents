# agents

Coleção de **subagentes** e **skills** customizados para o Claude Code, voltados ao projeto **Amavi Nutrição**.

## Estrutura

```
.
├── agents/   # subagentes (.md com frontmatter name/description/tools/model)
└── skills/   # skills reutilizáveis (a popular)
```

## Agentes disponíveis

| Agente | Quando usar | Modelo |
|---|---|---|
| [revisor-pr](agents/revisor-pr.md) | Antes de abrir PR/merge — revisa o diff contra `main` e flagra antipadrões do projeto. | sonnet |
| [revisor-seguranca](agents/revisor-seguranca.md) | Antes de commitar em controllers/services/configs — impede regressões de segurança já corrigidas. | sonnet |
| [caca-bugs](agents/caca-bugs.md) | **Depois** do `revisor-pr` — caça bugs de lógica de negócio, concorrência/estado e exceções engolidas num caminho específico. | haiku |
| [teste-funcional](agents/teste-funcional.md) | Depois de mudanças em controllers/services/regras de negócio — sobe a stack Docker e roda smoke tests HTTP. | sonnet |

Os quatro agentes são **complementares e não duplicam escopo** — o `caca-bugs` por exemplo evita explicitamente as áreas já cobertas pelos outros três.

## Como instalar

Os agentes seguem o formato de [subagente do Claude Code](https://docs.claude.com/en/docs/claude-code/sub-agents). Para usá-los, copie (ou crie um symlink) os arquivos de `agents/` para uma das duas localizações:

- **Projeto** (só nesse repo): `.claude/agents/`
- **Usuário** (em qualquer projeto): `~/.claude/agents/`

Exemplo no Windows (PowerShell), instalação por usuário:

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\agents" | Out-Null
Copy-Item agents\*.md "$HOME\.claude\agents\"
```

Depois, dentro do Claude Code, invoque pelo nome do frontmatter:

```
> use o revisor-pr
> caca-bugs em service/ConsultaService.java
```

## Skills

Pasta `skills/` reservada para skills customizadas (formato [Claude Code skills](https://docs.claude.com/en/docs/claude-code/skills)) — ainda sem conteúdo.
