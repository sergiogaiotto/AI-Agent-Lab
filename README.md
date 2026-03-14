# AI Agents Lab — Prof. Gaiotto

Curso Prático de Agentes de IA (16h) com LangGraph, LangChain e OpenAI.

Aplicação modular com 6 módulos progressivos, cada um construindo sobre o anterior.

## Arquitetura

```
ai-agents-course/
├── app/
│   ├── main.py              # FastAPI entry point
│   ├── config.py             # Configuração (.env)
│   ├── agents/
│   │   ├── __init__.py       # Utilitários compartilhados (get_llm)
│   │   ├── react_agent.py    # Módulo 1 — ReAct Agent
│   │   ├── codeact_agent.py  # Módulo 2 — CodeAct Agent
│   │   ├── search_agent.py   # Módulo 3 — DuckDuckGo Search
│   │   ├── reflection_agent.py # Módulo 4 — Self-Reflection
│   │   ├── multi_agent.py    # Módulo 5 — Multi-Agent Workflow
│   │   └── rag_agent.py      # Módulo 6 — Agentic RAG (FAISS)
│   └── routers/
│       └── agents.py         # API endpoints (FastAPI Router)
├── templates/
│   └── default.html          # Frontend SPA (Tailwind CSS)
├── .env                      # Variáveis de ambiente
├── requirements.txt          # Dependências Python
└── README.md
```

## Setup Rápido

```bash
# 1. Clonar / entrar no diretório
cd ai-agents-course

# 2. Criar ambiente virtual
python -m venv venv
# source venv/bin/activate  # Linux/Mac
venv\Scripts\activate   # Windows

# 3. Instalar dependências
pip install -r requirements.txt

# 4. Configurar API Key
# Editar .env com sua OPENAI_API_KEY
cp .env .env.local
# nano .env.local

# 5. Executar
uvicorn app.main:app --reload --port 8000
```

Acesse: http://localhost:8000

## Módulos do Curso

### Módulo 1 — ReAct Agent (Bloco 1)
- **Conceito**: Reasoning + Acting (Thought → Action → Observation)
- **Tools**: Calculadora, manipulação de texto
- **LangGraph**: StateGraph + ToolNode + conditional edges
- **Hands-on**: Construir o grafo de estados, adicionar tools, testar ciclo ReAct

### Módulo 2 — CodeAct Agent (Bloco 2)
- **Conceito**: O agente ESCREVE e EXECUTA código Python
- **Tools**: execute_python (sandbox)
- **LangGraph**: Mesmo padrão ReAct, com tool de execução de código
- **Hands-on**: Sandbox seguro, exec() com globals restritos

### Módulo 3 — Modern Tool: DuckDuckGo (Bloco 3)
- **Conceito**: Integração com APIs externas como ferramentas
- **Tools**: DuckDuckGoSearchResults (langchain-community)
- **LangGraph**: Tool binding com ferramentas externas
- **Hands-on**: Integrar busca web, processar resultados, citar fontes

### Módulo 4 — Self-Reflection (Bloco 4)
- **Conceito**: Generate → Reflect → Refine (iterativo)
- **Pattern**: Reflexion — crítica e auto-melhoria
- **LangGraph**: Grafo com loop condicional (iterações configuráveis)
- **Hands-on**: Construir nós generate/reflect/finalize, controlar iterações

### Módulo 5 — Multi-Agent Workflow (Bloco 5)
- **Conceito**: Supervisor orquestra agentes especializados
- **Agentes**: Researcher → Analyst → Writer
- **LangGraph**: Supervisor pattern com routing condicional
- **Hands-on**: Construir cada agente, implementar supervisor, routing

### Módulo 6 — Agentic RAG (Bloco 6)
- **Conceito**: Retrieval-Augmented Generation com agente
- **Features**: Upload, chunk_size, chunk_overlap, top_k, embedding
- **Stack**: FAISS + OpenAI Embeddings + LangGraph
- **Hands-on**: Upload docs, chunking, vector store, chat com KB

## API Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/` | Frontend SPA |
| GET | `/api/health` | Health check |
| POST | `/api/react` | ReAct Agent |
| POST | `/api/codeact` | CodeAct Agent |
| POST | `/api/search` | DuckDuckGo Search |
| POST | `/api/reflection` | Self-Reflection Agent |
| POST | `/api/multi-agent` | Multi-Agent Workflow |
| POST | `/api/rag/upload` | Upload documento para KB |
| GET | `/api/rag/knowledge-bases` | Listar KBs |
| DELETE | `/api/rag/knowledge-bases/{name}` | Excluir KB |
| POST | `/api/rag/chat` | Chat com KB |

## Stack Tecnológica

- **Backend**: Python 3.11+, FastAPI, Uvicorn
- **Agentes**: LangGraph, LangChain, LangChain-OpenAI
- **LLM**: OpenAI GPT-4o-mini (configurável)
- **Embeddings**: OpenAI text-embedding-3-small
- **Vector Store**: FAISS (CPU)
- **Busca Web**: DuckDuckGo Search
- **Frontend**: HTML5, Tailwind CSS, JavaScript vanilla
- **Design**: Identidade visual Fala Gaiotto (laranja + dark)

## Autor

**Sergio Gaiotto**
- Professor FIA lab.data
