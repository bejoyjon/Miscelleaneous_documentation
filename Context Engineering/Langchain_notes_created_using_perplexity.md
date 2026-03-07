# Comprehensive Teaching Notes: LangChain Deep Agents

## Deep Agents overview

Deep agents are a Python-based framework for building autonomous agents powered by large language models (LLMs). They're designed as the easiest way to start building agents and applications with built-in capabilities for task planning, file systems for context management, subagent-spawning, and long-term memory. The deepagents library is built on top of LangChain's core building blocks and uses the LangGraph runtime for durable execution, streaming, and human-in-the-loop features.

**Key Components:**
- **Deep Agents SDK**: A package for building agents that can handle any task
- **Deep Agents CLI**: A terminal coding agent built on the deepagents package

**When to Use Deep Agents:**
- Handling complex, multi-step tasks requiring planning and decomposition
- Managing large amounts of context through file system tools
- Swapping filesystem backends (in-memory, local disk, durable stores, sandboxes)
- Delegating work to specialized subagents for context isolation
- Persisting memory across conversations and threads

## Quickstart

Getting started with Deep Agents involves these key steps:

**Prerequisites:**
- API key from a model provider (Anthropic, OpenAI, etc.)
- Models must support tool calling

**Basic Setup:**
1. Install dependencies: `pip install deepagents tavily-python`
2. Set up API keys (ANTHROPIC_API_KEY, TAVILY_API_KEY)
3. Create a search tool using an external provider like Tavily
4. Create a deep agent with `create_deep_agent()` function
5. Invoke the agent with user messages

**How It Works Automatically:**
- Plans its approach using the built-in `write_todos` tool to break down research tasks
- Conducts research by calling tools like `internet_search`
- Manages context by using file system tools (`write_file`, `read_file`) to offload large content
- Spawns subagents as needed to delegate complex subtasks
- Synthesizes findings into coherent responses

**Advanced Features:**
- Built-in streaming for real-time updates
- Support for long-term persistent memory across conversations
- Deployment options via LangGraph Platform or self-hosting

## Customize Deep Agents

The `create_deep_agent()` function supports several core configuration options:

**1. Model**
- Specify any LangChain chat model that supports tool calling
- Can use provider:model format (e.g., "openai:gpt-5.3-codex")
- Can pass `init_chat_model()` or direct model instances
- Configure model-specific parameters (like thinking budgets for Claude)

**2. Tools**
- Pass callable functions as tools to the agent
- Tools must have proper docstrings and type hints
- Can be custom functions or provider-specific tools

**3. System Prompt**
- Customize agent behavior with custom system prompts
- Provides instructions for how the agent should behave

**4. Middleware**
- Composable middleware for custom behaviors
- Allows extending agent capabilities

**5. Subagents**
- Delegate work to specialized subagents
- Keep main agent context clean

**6. Backends (Virtual Filesystems)**
- Choose storage backend (in-memory, local disk, LangGraph store, sandboxes)
- Pluggable architecture allows custom implementations

**7. Human-in-the-Loop**
- Pause agent execution at specified operations
- Allow user approval before sensitive actions

**8. Skills**
- Specialized capabilities that can be loaded progressively
- Reduces token usage by only loading relevant skills

**9. Memory**
- Enable persistent memory using AGENTS.md files
- Agent can update memory based on interactions

## Comparison with Claude Agent SDK and Codex

**LangChain Deep Agents:**
- **Use cases**: Custom general-purpose agents (including coding)
- **Model support**: Flexible and model-agnostic (Anthropic, OpenAI, 100+ others)
- **Architecture**: Python SDK, TypeScript SDK, and CLI
- **Execution**: Local, remote sandboxes, virtual filesystem
- **Deployment**: LangSmith Platform
- **Frontend**: Integration with React
- **Observability**: LangSmith tracing & evaluations
- **Security**: Composable, per-tool human-in-the-loop
- **License**: MIT

**Claude Agent SDK:**
- **Use cases**: Custom AI coding agents
- **Model support**: Tightly integrated with Claude models
- **Security**: Permission system with modes, rules and hooks
- **License**: MIT (underlying Claude Code is proprietary)

**Codex SDK:**
- **Use cases**: Prebuilt coding agent that can execute coding tasks
- **Model support**: Tightly integrated with OpenAI (GPT-5.3-Codex)
- **Security**: Built-in tiers using approval modes and OS-level sandboxes

**Key Differentiators:**
- Long-term memory via Memory Store
- Sandbox-as-tool pattern with different providers
- Virtual filesystem with pluggable backends
- Production deployment via LangSmith
- LangSmith native tracing and debugging

## Models

Deep agents work with any LangChain chat model that supports tool calling.

**Specifying Models:**
- Simplest approach: Pass a model string in "provider:model" format
- Example: `agent = create_deep_agent(model="openai:gpt-5.3-codex")`
- Internally calls `init_chat_model()` with default parameters

**Configuring Model Parameters:**
- Use `init_chat_model()` for advanced configuration
- Can pass direct model instances like `ChatOpenAI(model="gpt-5")`
- Configure provider-specific parameters (e.g., thinking budgets for Claude)

**Supported Models:**
- Any chat model supporting tool calling
- Check LangChain's chat model integrations for full list

## Harness capabilities

The agent harness is a combination of different tools and features that enable agents to handle complex tasks. Key capabilities include:

**1. Planning and Task Decomposition**
- Built-in `write_todos` tool lets agents break complex tasks into discrete steps
- Track task progress with statuses (pending, in_progress, completed)
- Helps agents organize complex multi-step work
- Useful for long-running tasks and planning

**2. Virtual Filesystem Access**
- `ls` - List files in directory with metadata
- `read_file` - Read file contents with line numbers (supports images)
- `write_file` - Create new files
- `edit_file` - Perform exact string replacements
- `glob` - Find files matching patterns
- `grep` - Search file contents with multiple output modes
- `execute` - Run shell commands (requires sandbox backends)

**3. Task Delegation (Subagents)**
- Create ephemeral subagents for specialized work
- **Benefits**:
  - Context isolation - Main agent's context stays clean
  - Parallel execution - Multiple subagents can run concurrently
  - Specialization - Different tools/configurations per subagent
  - Token efficiency - Large subtask context compressed into single report
- Default "general-purpose" subagent available with filesystem tools
- Can create custom specialized subagents

**4. Context Management**
- **Input context**: System prompts, base agent prompt, memory, skills
- **Runtime context**: Context compression through offloading and summarization
- **Offloading**: Automatically saves large tool inputs/results to filesystem
- **Summarization**: LLM generates structured summary when context size exceeds limit
- Keeps 10% of tokens as recent context
- Falls back to 170,000-token trigger if model profile unavailable

**5. Code Execution**
- When using sandbox backend, exposes `execute` tool
- Runs in isolated environments for security
- Provides clean environments with specific dependencies
- Returns stdout/stderr, exit code, and execution time

**6. Human-in-the-Loop**
- Pause agent execution at specified tool operations via `interrupt_on`
- Useful for safety gates on destructive operations
- User verification before expensive API calls
- Interactive debugging and guidance

**7. Skills**
- Provide specialized capabilities following Agent Skills standard
- Skills have SKILL.md files with descriptions
- Progressive disclosure - only loaded when needed
- Reduces token usage by only loading relevant skills

**8. Memory**
- Supports persistent memory files using AGENTS.md format
- Memory always loaded (unlike skills which are lazy-loaded)
- Agent can update memory based on interactions
- Provides persistent context across conversations

## Backends

Backends are pluggable filesystem implementations that determine how files are stored and accessed by agents.

**Built-in Backends:**

1. **StateBackend (Ephemeral)**
   - Stores files in LangGraph agent state
   - Persists only within single thread
   - Files lost when thread ends
   - Best for: Scratch pad for agent work

2. **FilesystemBackend (Local Disk)**
   - Grants agents direct filesystem read/write
   - Appropriate for: Local development CLIs, CI/CD pipelines
   - Security risks: Can read any accessible file, modifications permanent
   - Safeguards: Enable human-in-the-loop, exclude secrets, use sandboxes

3. **LocalShellBackend (Local Shell)**
   - Filesystem access + shell execution via `execute` tool
   - Appropriate for: Local development CLIs, personal environments
   - Security risks: Execute arbitrary commands with user's permissions
   - Strongly recommended: Enable human-in-the-loop middleware

4. **StoreBackend (LangGraph Store)**
   - Stores files in persistent LangGraph Store
   - Persists across all threads and conversations
   - Best for: Production deployments via LangSmith
   - When omitting store parameter, platform provides it automatically

5. **CompositeBackend (Router)**
   - Routes file operations to different backends based on path prefixes
   - Preserves original path prefixes in listings
   - Enables both ephemeral and persistent storage

**Specifying Backends:**
- Pass to `create_deep_agent(backend=...)`
- Can pass instance implementing BackendProtocol or factory function
- Default: `lambda rt: StateBackend(rt)`

**Routing Example:**
```
CompositeBackend(
    default=StateBackend(rt),  # Ephemeral
    routes={"/memories/": StoreBackend(rt)}  # Persistent
)
```

**Custom Backends:**
- Implement BackendProtocol with required endpoints
- `ls_info`, `read`, `grep_raw`, `glob_info`, `write`, `edit`
- Can project remote stores (S3, Postgres) as virtual filesystems

## Subagents

Subagents are specialized agents that main agents can spawn to handle specific tasks while keeping context clean.

**Why Use Subagents:**
- Solve the "context bloat problem"
- Agents using tools with large outputs fill context window quickly with intermediate results
- Subagents isolate this detailed work - main agent receives only final report

**When to Use:**
- ✅ Multi-step tasks that would clutter main agent's context
- ✅ Specialized domains needing custom instructions
- ✅ Tasks requiring different model capabilities
- ❌ Simple, single-step tasks
- ❌ When you need to maintain intermediate context

**Configuration:**

Subagents can be defined as dictionaries with fields:
- **name** (str): Unique identifier for the subagent
- **description** (str): What this subagent does (used by main agent to decide when to delegate)
- **system_prompt** (str): Instructions for the subagent
- **tools** (list[Callable]): Tools the subagent can use
- **model** (optional): Override main agent's model
- **middleware** (optional): Additional middleware for custom behavior
- **interrupt_on** (optional): Human-in-the-loop configuration
- **skills** (optional): Skill source paths

**CompiledSubAgent:**
- For complex workflows, use pre-built LangGraph graphs
- Must call `.compile()` on the graph
- Requires state key "messages"

**Special: General-Purpose Subagent**
- Automatically available in addition to user-defined subagents
- Has same system prompt as main agent
- Has access to all same tools
- Uses same model (unless overridden)
- Inherits skills from main agent
- Can be overridden with `name="general-purpose"`

**Skills Inheritance:**
- General-purpose subagent: Automatically inherits skills
- Custom subagents: Do NOT inherit skills by default - use `skills` parameter

**Best Practices:**
- Write clear, specific descriptions for main agent to decide when to delegate
- Keep system prompts detailed with specific guidance
- Minimize tool sets - only give subagents tools they need
- Choose models by task - different models excel at different capabilities
- Return concise results from subagents - instruct to return summaries

**Context Management:**
- All subagents receive same parent context
- Use namespaced keys for per-subagent context
- Identify which subagent called a tool via `lc_agent_name` in tracing

## Long-term memory

Long-term memory enables agents to persist information across conversations and threads.

**Overview:**
- Default filesystem is transient (single thread)
- Extend with persistent memory using CompositeBackend
- Routes files under `/memories/` to StoreBackend for persistence

**Architecture:**

1. **Short-term (Transient) Filesystem**
   - Stored in agent's state (StateBackend)
   - Persists only within single thread
   - Files lost when thread ends
   - Standard paths: `/notes.txt`, `/workspace/draft.md`

2. **Long-term (Persistent) Filesystem**
   - Stored in LangGraph Store (StoreBackend)
   - Persists across all threads and conversations
   - Survives agent restarts
   - Paths prefixed with `/memories/`: `/memories/preferences.txt`

**Path Routing:**
- CompositeBackend routes based on path prefixes
- Files starting with `/memories/` stored in persistent Store
- Other files remain in transient state
- All filesystem tools work with both systems
- CompositeBackend strips prefix before storing (e.g., `/memories/preferences.txt` stored as `/preferences.txt`)

**Setup Example:**
```python
from deepagents.backends import CompositeBackend, StateBackend, StoreBackend
from langgraph.store.memory import InMemoryStore

def make_backend(runtime):
    return CompositeBackend(
        default=StateBackend(runtime),  # Ephemeral
        routes={"/memories/": StoreBackend(runtime)}  # Persistent
    )

agent = create_deep_agent(
    store=InMemoryStore(),
    backend=make_backend,
    checkpointer=checkpointer
)
```

**Cross-Thread Persistence:**
- Files in `/memories/` accessible from any thread
- Use different thread IDs to create separate sessions
- Each thread can read/write to same persistent location

**Store Implementations:**
- **InMemoryStore** (development): Quick testing, data lost on restart
- **PostgresStore** (production): Persistent storage in database
- Any LangGraph BaseStore implementation works

**Use Cases:**
1. **User preferences**: Store across sessions
2. **Self-improving instructions**: Agent updates its own instructions based on feedback
3. **Knowledge base**: Build knowledge over multiple conversations
4. **Research projects**: Maintain research state across sessions

**FileData Schema:**
Files stored use schema with:
- `content` - List of strings (one per line)
- `created_at` - ISO 8601 timestamp
- `modified_at` - ISO 8601 timestamp

**Best Practices:**
- Use descriptive paths: `/memories/user_preferences.txt`, `/memories/research/topic_a/notes.txt`
- Document the memory structure in system prompt
- Implement periodic cleanup of outdated persistent data
- Choose right storage: InMemoryStore for dev, PostgresStore for production
- Consider assistant_id-based namespacing for multi-tenant scenarios

***

**Summary for Understanding:**
Deep Agents represent a modern approach to building AI agents that combines task planning, flexible file system management, context isolation through subagents, and persistent memory. This comprehensive framework allows agents to handle complex real-world tasks while maintaining clean execution environments and learning from past interactions.