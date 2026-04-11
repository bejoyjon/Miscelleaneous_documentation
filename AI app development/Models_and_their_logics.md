# Foundation models
## Core tech behind models
### Notes from [ByteByteGo Gen AI series](https://bytebytego.com/courses/genai-system-design-interview/introduction-and-overview)
Add here

## FAQs
### 1. What are the criteria that decides speed of training / finetuning?
Add here


## Key sites
1. Manus.im - does basic reasearch for free, creates reports and makes a "web app" for showing the info. Can add apps or connectors to most major apps like Gmail, Outlook (no Teams though), maybe the most important one is connecting to the browser and controlling it for doing the search and displaying web app and all - https://manus.im/app#connectors/built-in
2. Minimax.io - distillation trained on Claude, almost meets Opus 4.6 scores as of 2026 Feb. Offering "coding plan" instead of tokens for $10-$50. https://platform.minimax.io/subscribe/coding-plan
3. Google AI studio - one of the very few better known models accessible from internal firewall - https://aistudio.google.com/



## Local and free LLMs
By running models locally, users benefit from full data privacy, no subscription costs, and no usage limits.

### Llama.cpp
[Llama.cpp](https://www.youtube.com/watch?v=P8m5eHAyrFM) is an inference engine (like an LLM processor) designed to run LLMs on consumer hardware like laptops / Raspberry Pis (0:00-0:36). 

#### Logic
___High Precision (Original State) vs Quantization Process____: This format also trades off quantization size (high-precision formats, such as 16-bit or 32-bit (4:48) to a 4-bit (5:10)) for precision size, relying on disproportionate reduction in size vs performance. This reduction in precision allows the model to require significantly less RAM to run — only 25% of the original hardware capabilities — while maintaining similar capabilities and a high degree of accuracy (5:22). This process is facilitated by the GGUF format, which packages the quantized weights and metadata into a single file for quick loading and swapping (4:15-4:35). 
 

#### How it works:
- Get model from Source / Repository: Models like DeepSeek, Llama, and Qwen are obtained from repositories like Hugging Face (4:00).
- Convert to ___GGUF Format___: Converted to GGUF format (4:10) which packages the model's weights and metadata together into a single file, making it highly efficient for quickly loading and swapping between different models (4:23).
- ___Quantization Variants___ - Models are named based on their quantization type, such as Q4_K_M (5:51). This specific notation refers to 4-bit precision (Q4) combined with a specific compression algorithm variant (K_M) tuned for quality (6:12).
- ___Optimized Performance___: The engine utilizes optimized kernels for various platforms, including Metal (Mac), CUDA (Nvidia), ROCm (AMD), and standard CPUs (6:39-7:11).
- ___Implementation___: Developers can use Llama.cpp via CLI or setting up an OpenAI-compatible local server on a specific port (7:14-7:54). ___<== How can I integrate it into my AI ecosystem? Is a download and use via Illama possible?___
- ___Advanced Features___: Support for multimodal capabilities (interpreting images) and Model Context Protocol to connect to external data sources like CRMs (8:10-8:33).

### Gemma 4
