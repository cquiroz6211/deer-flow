# AGENTS.md — deerflow/backend

## OVERVIEW
DeerFlow backend: LangGraph-based AI super agent with sandbox execution, memory, and extensible tools.

## STRUCTURE
```
backend/src/
├── agents/lead_agent/     # Main LangGraph agent factory
├── agents/middlewares/    # 9 middleware components
├── agents/memory/         # LLM-powered persistent memory
├── gateway/routers/      # FastAPI REST endpoints
├── sandbox/               # Isolated code execution
├── subagents/             # Background task delegation
└── tools/builtins/        # Built-in tools
```

## WHERE TO LOOK
- **Agent Creation**: `src/agents/lead_agent/` — `make_lead_agent()` factory
- **Middleware Chain**: 9 ordered middlewares (thread data → uploads → sandbox → summarization → todos → title → memory → view image → clarification)
- **Gateway API**: `src/gateway/app.py` — FastAPI entry point
- **Sandbox System**: `src/sandbox/` — abstract interface with Local/Docker providers
- **Subagents**: `src/subagents/` — async parallel execution

## CONVENTIONS
- Python 3.12+ with type hints
- Line length: 240 chars
- Linter: `ruff`
- Double quotes for strings
- 4-space indentation

## ANTI-PATTERNS
- ❌ Don't skip middleware order — they're strictly sequential
- ❌ Don't call LLM in middleware init — only in `invoke()`
- ❌ Don't use synchronous file I/O in agent thread — use async methods
- ❌ Don't hardcode tool names — use registry pattern

## COMMANDS
```bash
make install   # Install deps
make dev       # Run LangGraph (port 2024)
make gateway   # Run Gateway API (port 8001)
make lint      # Run ruff
```