# Retrieval Augmented Generation Methodology
1. Key step is to identify all the data sources and their relationships, within the larger logic of tying together multiple pieces of information. ___Therefore, critical to identify, understand, develop / improve data existing sources for any organization we work for.___ Even better if we can design for the future e.g a distinct data group for AI generated data.
2. Create an Index of sorts (tree, semantic, chronological, linear or a combo of these) - use this for faster and more accurate search. Test if 2 or 3 separate indices point to the same doc. The indices should be human modifiable.
   3. Make sure there are role based rights for read vs edit as the indices now form part of critical / "nuclear" set of data points. 
4. Data handling system should manage outdated knowledge. For e.g. checking two documents for similarity in title, purpose and other metadata. If over X% similar, then mark older doc as outdate in Index. This data also should be human manageable.
5. Generic approach to RAG:
   - read data
   - chunk it using overlapping chunking models
   - store it in a vector database
   - make an index from chunk ID / vector store ID vs text.
       - Tree indexing is a highly accurate but resource intensive method. Same logic as tree search.
   - Use the vector store data for similarity matching when user prompts.

Rajsuthan Gopinath has done a [PoC for RAGing](https://www.youtube.com/watch?v=bkKVWf7qQUk&list=PLA1G2nVay86RW7LqJERpgTAWbWmNdXcAI) from 10k+ docs from NASA for an aerospace co. Detailed notes [here](https://github.com/bejoyjon/Miscelleaneous_documentation/blob/main/Context%20Engineering/Large_doc_store_RAG_by_Rajsuthan_Gopinathan.md).\
Challenges:
1. Mix of scans, technical diagrams meant large amount of image detection.
2. Required hybrid retreival methods, formula detection.




# Tools
## MCPs
### How to create one

## [Langchain](https://docs.langchain.com)
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
     - TodoListMiddleware: todo lists for organizing agent tasks and work.
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
#### [Linksmith](https://youtu.be/QZjjVMhjEcY) 
Can take in images in Base 64 format in the traces - set up for image relevancy to determine if an uploaded image is relevant to the product ecosystem, can apply filter  for traces with image inputs. Multimodal files can be sent as attachments to traces or as part of an offline data set, in addition to natively passing base64 format. The attachment file is mapped in the human message using the 'attachments' variable, allowing for mapping of all attachments or specific ones by name.





# Appendix
## FAQs
### 1. Context windows seem to vary by model, and by each generation. What decides context window, speed of training and speed of inference at the model level and infra? Is there any impact of vector databases or similar harnesses?
Context window - \
Speed of training - \
[Speed of training](https://github.com/bejoyjon/Miscelleaneous_documentation/blob/main/AI%20apps%20/Noteworthy_web_apps_and_models.md#1-what-are-the-criteria-that-decides-speed-of-training--finetuning)

### 2. 

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
