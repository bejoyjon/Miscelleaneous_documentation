# General Architecture

## Local architecture 
### Simple

### Docker

## Cloud architecture

### Using Kubernetes


# Development
## Best Practices
### Preventing Slop with AI Agents
Hooks are crucial for agentic engineering, allowing for custom harnesses, logging, and preventing destructive changes as a first layer of defense. Quality gates enforce strict linting, type-checking, and test passing for LLMs, ensuring code adheres to project standards. An anti-mocking testing philosophy is adopted to ensure that tests written by LLMs are genuinely testing the actual code, not just mocked components. High test coverage and a 100% pass rate are maintained, with any failing tests or agent-written failures immediately addressed.

### Standardization and Isolation in Agent Workflows
Standardization ensures all issues and agent learnings are tracked in one location, preventing scattered files and promoting organized work. Standardizing where agents perform their work, often through work trees, and establishing review processes for agent output are crucial for maintaining codebase quality. Per-agent isolation is vital for multi-agent workflows and swarms, preventing agents from interfering with each other's work. Running agents within work trees ensures isolation, a guiding principle that an isolated agent is a safe agent, especially with multiple agents working on a codebase.

### Hard Blocks and Hooks for Agent Control
The segment introduces hard blocks as a crucial tool to define actions AI agents should never be allowed to perform, such as blocking 'git push' to prevent unauthorized remote pushes. It emphasizes blocking specific tools for different agents, like restricting a scout agent to only read files and not write them, to ensure focused behavior. The discussion then shifts to how to force correct behavior, ensuring agents stick to their assigned tasks and are reset if they deviate. Hard blocks are closely tied to hooks, which allow these restrictions to be established and enforced as code, although this list is not exhaustive of all available tools.

### Ensuring Anti-Slop Philosophy in AI Agents
Traceability, including hooks, is crucial for tracking agent actions and changes to ensure an anti-slop philosophy. Task decomposition emphasizes that a focused agent is a correct agent, ideally handling one task with one prompt for better results. Placing trust in agents increases when their success rate is high with a 'one agent, one task, one prompt' approach, demonstrating their focus and effectiveness. The 'pit of success' technique is vital for agentic engineering, as passing high-quality input tokens to LLMs leads to higher quality code output in a recursive loop.

### Ensuring Quality in AI Agent Workflows
Specs should be unambiguous and perfectly aligned with the vision, requiring detailed outlines and potentially code snippets to ensure agent productivity. Multi-agent workflows or swarms involve agents decomposing tasks and reviewing each other's code, with every step requiring high-quality checks before passing work to the next agent. By ensuring quality checks at every stage, from passing tests and linting to typing, the coordinator agent receives code free of "slop". Agent scope is crucial, advocating for one agent, one task, and one prompt, clearly defining what files an agent should work on and reducing ambiguity by specifying what is outside its scope.

### Standardization and Best Practices for Agentic Engineering
Standardization is crucial for agents, ensuring their output and behavior are predictable and consistent across the codebase. For agent swarms, a clear chain of command is vital, defining when user intervention is needed and when developers should be notified of issues to prevent producing low-quality code. The speaker advises teams to collaboratively define their own tools and techniques for agent workflows rather than blindly adopting external solutions.
