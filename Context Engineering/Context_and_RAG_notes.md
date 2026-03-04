## General notes
1. Key step is to identify all the data sources and their relationships, within the larger logic of tying together multiple pieces of information.
2. Generic approach to RAG:
   - read data
   - chunk it using overlapping chunking models
   - store it in a vector database
   - make an index from chunk ID / vector store ID vs text.
       - Tree indexing is a highly accurate but resource intensive method. Same logic as tree search.
   - Use the vector store data for similarity matching when user prompts.

## Langchain notes (https://docs.langchain.com/)
### Deepagents

### Langchain

### Langsmith

### Langgraph


### Evals

