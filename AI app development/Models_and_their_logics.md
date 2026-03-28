# Foundation models

## Key sites
1. Manus.im - does basic reasearch for free, creates reports and makes a "web app" for showing the info. Can add apps or connectors to most major apps like Gmail, Outlook (no Teams though), maybe the most important one is connecting to the browser and controlling it for doing the search and displaying web app and all - https://manus.im/app#connectors/built-in
2. Minimax.io - distillation trained on Claude, almost meets Opus 4.6 scores as of 2026 Feb. Offering "coding plan" instead of tokens for $10-$50. https://platform.minimax.io/subscribe/coding-plan
3. Google AI studio - one of the very few better known models accessible from internal firewall - https://aistudio.google.com/

## Core tech behind models
Add here

# FAQs
### 1. What are the criteria that decides speed of training / finetuning?
Add here

## Local and free LLMs
[This video](https://www.youtube.com/watch?v=P8m5eHAyrFM) introduces Llama.cpp, an inference engine designed to run Large Language Models (LLMs) on consumer hardware like laptops or Raspberry Pis rather than expensive cloud data centers (0:00-0:36). By running models locally, users benefit from full data privacy, no subscription costs, and no usage limits.
Key topics covered include:
Retrieval Augmented Generation (RAG): Connecting LLMs to private documents (PDFs, spreadsheets) to provide context-aware answers without sending data to the cloud (0:40-1:06).
___Model Quantization (GGUF Format)___: Llama.cpp compresses high-precision models (16-bit or 32-bit) down to lower precision (e.g., 4-bit) using the GGUF format. This reduces RAM requirements by up to 75% while maintaining high accuracy (4:08-5:24). This achieved through:
- Model Source & Repository: Models are typically obtained from repositories like Hugging Face (4:00), featuring various architectures like DeepSeek, Llama, and Qwen.
- ___GGUF Format___: Llama.cpp uses a specific file format called GGUF (4:10). This format packages the model's weights and metadata together into a single file, making it highly efficient for quickly loading and swapping between different models (4:23). 
- ___High Precision (Original State) vs Quantization Process____: OG Models are often released in high-precision formats, such as 16-bit or 32-bit (4:48). While this ensures high accuracy, it requires immense amounts of RAM to store and run the model (4:59). Quantization Process shrinks the model down to a lower precision, such as 4-bit (5:10). This reduces the hardware requirements significantly. How does quantization shrink AI models? Quantization shrinks AI models by reducing the precision of the model's weights and metadata (4:45). The process involves transforming the model from a high-precision format, such as 16-bit or 32-bit, down to a lower precision, specifically 4-bit (5:08).This reduction in precision allows the model to require significantly less RAM to run—only 25% of the original hardware capabilities—while maintaining similar capabilities and a high degree of accuracy (5:22). This process is facilitated by the GGUF format, which packages the quantized weights and metadata into a single file for quick loading and swapping (4:15-4:35). ___Quantization Variants___ - Models are named based on their quantization type, such as Q4_K_M (5:51). This specific notation refers to 4-bit precision (Q4) combined with a specific compression algorithm variant (K_M) tuned for quality (6:12).
- ___Optimized Performance___: The engine utilizes optimized kernels for various platforms, including Metal (Mac), CUDA (Nvidia), ROCm (AMD), and standard CPUs (6:39-7:11).
- ___Implementation___: Developers can use Llama.cpp via the command-line interface or by setting up an OpenAI-compatible local server on a specific port (7:14-7:54).
- ___Advanced Features___: Support for multimodal capabilities (interpreting images) and Model Context Protocol to connect to external data sources like CRMs (8:10-8:33).
