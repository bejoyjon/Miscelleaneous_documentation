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
Built on Langchain's core blocks. Execution, streaming etc. through LangGraph. \
- Deep Agents SDK - python package for e.g.
- Deep Agents CLI - what I use from CLI\
[Sample code](#deepagents-sample)

### Langchain

### Langsmith

### Langgraph


### Evals


## Sample code
### Deepagents sample
```# pip install -qU deepagents
from deepagents import create_deep_agent

def get_weather(city: str) -> str:
    """Get weather for a given city."""
    return f"It's always sunny in {city}!"

agent = create_deep_agent(
    tools=[get_weather],
    system_prompt="You are a helpful assistant",
      )

# Run the agent
agent.invoke(
    {"messages": [{"role": "user", "content": "what is the weather in sf"}]}
)
```
