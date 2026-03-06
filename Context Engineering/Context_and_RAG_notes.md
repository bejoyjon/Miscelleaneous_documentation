## Retrieval Augmented Generation
1. Key step is to identify all the data sources and their relationships, within the larger logic of tying together multiple pieces of information.
2. Generic approach to RAG:
   - read data
   - chunk it using overlapping chunking models
   - store it in a vector database
   - make an index from chunk ID / vector store ID vs text.
       - Tree indexing is a highly accurate but resource intensive method. Same logic as tree search.
   - Use the vector store data for similarity matching when user prompts.
  
## MCPs
### How to create one

## [Langchain notes](https://docs.langchain.com)
### Deepagents
Basically agent harness i.e. tool calling loop like OpenAI or Claude agents, but has a lot more integrations built in. \
Built on Langchain's core blocks. Execution, streaming etc. through LangGraph.
- Deep Agents SDK - python package for e.g.
- Deep Agents CLI - what I use from CLI
[Sample code](#deepagents-sample)

#### ___Benefits___:
- Manages large context as a system using file system tools. __ls__, __read_file__, __write_file__, __edit_file__.
- Swap filesystem backends from its ___virtual filesystem___ - in-memory state, local disk, durable stores or your own custom backend, even sandboxes such as Modal or Daytona.
- Persistant memory across sessions, using LangGraph's Memory Store.
- Multistep process planning and handling. __write_todos__ . Does this on its own if it feels the need, just like calling tools.

#### ___Features___:
- Streaming - sending updates as agent executes it. Useful for both output and debugging.
- Spawn new agents - subagents can be configured with their own system_prompt, tools and even models separate from the default, which is the master agent's model.
- Defaults - Model - Claude x.x (changes every now and then), System prompt - mostly about tool use, and subagents. Middleware special tools like filesystem tools can be appended to the system prompt as well. The system prompt does not define any kind of role, only generic, all purpose instructions.
- [Middleware tools](#deepagents-middleware-sample)
      - TodoListMiddleware: todo lists for organizing agent tasks and work
      - FilesystemMiddleware: file system operations such as reading, writing, and navigating directories
      - SubAgentMiddleware: Spawns and coordinates subagents for delegating tasks to specialized agents
      - SummarizationMiddleware: Condenses message history to stay within context limits when conversations grow long
      - AnthropicPromptCachingMiddleware: Auto reduction of redundant token processing when using <ins>Anthropic</ins> models
      - PatchToolCallsMiddleware: Automatic message history fixes when tool calls are interrupted or cancelled before receiving results
   - Human in the loop middleware tools   
      - MemoryMiddleware: Persists and retrieves conversation context across sessions when the memory argument is provided
      - SkillsMiddleware: Enables custom skills when the skills argument is provided
      - HumanInTheLoopMiddleware: Pauses for human approval or input at specified points when the interrupt_on argument is provided
      - More middleware can be integrated with custom hooks - see [deepagents custom middleware docs](https://docs.langchain.com/oss/python/langchain/middleware/custom#custom-state-schema), note possible errors that you can make
- Backends
   - default - StateBackend, lasts for the session only.
   - Filesystembackend - dealing with local files
   - LocalShellBackend - shell interactions
   - StoreBackend - 
   - CompositeBackend
   - Sandbox - special type of Backend which makes changes in a constrained environment.


#### ___Do not use Deepagents if___ :
- when is deepagents NOT the best solution to use



### Langchain

### Langsmith

### Langgraph


### Evals


## Sample code
### Deepagents sample
```
# pip install -qU deepagents
from deepagents import create_deep_agent
import os
from typing import Literal
from tavily import TavilyClient
from deepagents import create_deep_agent

tavily_client = TavilyClient(api_key=os.environ["TAVILY_API_KEY"])

# CREATE AN INTERNET SEARCH TOOL USING TAVILY
def internet_search(
    query: str,
    max_results: int = 5,
    topic: Literal["general", "news", "finance"] = "general",
    include_raw_content: bool = False,
):
    """Run a web search"""
    return tavily_client.search(
        query,
        max_results=max_results,
        include_raw_content=include_raw_content,
        topic=topic,
    )

# SOME GENERIC TOOL
def get_weather(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

# _Set LANGSMITH_TRACING=true and your API key to get started_
agent = create_deep_agent(
    tools=[internet_search, get_weather],
    system_prompt="You are a helpful assistant",
      )

# Run the agent
agent.invoke(
    {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
)
```
### Deepagents middleware sample
```
from langchain.tools import tool
from langchain.agents.middleware import wrap_tool_call
from deepagents import create_deep_agent


@tool
def get_weather(city: str) -> str:
    """Get the weather in a city."""
    return f"The weather in {city} is sunny."


call_count = [0]  # Use list to allow modification in nested function

@wrap_tool_call
def log_tool_calls(request, handler):
    """Intercept and log every tool call - demonstrates cross-cutting concern."""
    call_count[0] += 1
    tool_name = request.name if hasattr(request, 'name') else str(request)

    print(f"[Middleware] Tool call #{call_count[0]}: {tool_name}")
    print(f"[Middleware] Arguments: {request.args if hasattr(request, 'args') else 'N/A'}")

    # Execute the tool call
    result = handler(request)

    # Log the result
    print(f"[Middleware] Tool call #{call_count[0]} completed")

    return result


agent = create_deep_agent(
    tools=[get_weather],
    middleware=[log_tool_calls],
)
```
