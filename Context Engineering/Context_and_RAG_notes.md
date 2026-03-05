## General notes
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

## Langchain notes (https://docs.langchain.com/)
### Deepagents
Basically agent harness i.e. tool calling loop like OpenAI or Claude agents, but has a lot more integrations built in. \
Benefits:
- Manages large context as a system using file system tools. __ls__, __read_file__, __write_file__, __edit_file__.
- Swap filesystem backends from its ___virtual filesystem___ - in-memory state, local disk, durable stores or your own custom backend, even sandboxes such as Modal or Daytona.
- Persistant memory across sessions, using LangGraph's Memory Store.
- Multistep process planning and handling. __write_todos__


Built on Langchain's core blocks. Execution, streaming etc. through LangGraph.
- Deep Agents SDK - python package for e.g.
- Deep Agents CLI - what I use from CLI\
[Sample code](#deepagents-sample)

### Langchain

### Langsmith

### Langgraph


### Evals


## Sample code
### Deepagents sample
```
# pip install -qU deepagents
from deepagents import create_deep_agent

def get_weather(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

# _Set LANGSMITH_TRACING=true and your API key to get started_
agent = create_deep_agent(
    tools=[get_weather],
    system_prompt="You are a helpful assistant",
      )

# Run the agent
agent.invoke(
    {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
)
```
