
## [PART 1 - Building a Scalable RAG System for Rocket Science Documents](https://www.youtube.com/live/bkKVWf7qQUk?si=YL2UrWcjZH18B9SZ)
### Outline of the Video Content
Introduction: Background and Project Scope
Use Case Description: Meridian Aerospace and Data Challenges
Domain Exploration: AI-Assisted Understanding with Claude
User Personas and System Success Criteria
Document Characteristics and Visual Exploration
Technology Stack: Dockling, Vector DB, VLMs, and Phased Development
Document Processing: Table Detection and Extraction
Table Representation: Markdown vs JSON, Image Support, and Model Comparisons
Formula Extraction: Cropping, VLM Processing, Challenges, and Solutions
General Observations: Confidence Scoring, Evaluation, and Next Steps
Wrap-Up: Future Work and Repository Sharing

### Key steps for analysis
#### 🚀 Project Introduction and Use Case
Raj introduces himself and outlines his experience with AI agents in regulated enterprises such as pharma and banks. The project focuses on building a Retrieval-Augmented Generation (RAG) system for complex NASA rocket science documents. Initial scope: processing 10,000 documents, scalable to 85,000+, including scanned tables, formulas, technical jargon, and diagrams. Raj presents a fictional but realistic use case based on Meridian Aerospace, a midsize aerospace engineering consultancy with 180 employees. Over 25 years, they accumulated approximately 85,000 documents, including propulsion test reports, safety analyses, failure investigations, specifications, and compliance filings dating back to the 1990s. Engineers currently spend 4-6 hours per project searching archives;  retiring senior engineers’ minds, and missed information has led to failures in safety reviews. The system aims to reduce search time drastically and improve accuracy in retrieving technical data, including mathematical equations and technical diagrams, at scale.

#### 🔍 Domain & User Insights
Challenges include heavy use of scanned documents (40%), highly technical documents, including scanned records, complex tables, formulas, and interconnected references. Semantic search is essential; keyword search fails due to domain-specific terminology and jargon. Two main user personas: <ins>Sandra (experienced engineer needing precise validation) and a junior engineer, unnamed, but let's call him Chris (requiring proactive guidance)</ins>. Accuracy is paramount; vague or assumed answers are unacceptable due to safety and regulatory concerns. The system must ask clarifying questions and avoid assumptions, supporting iterative refinement. Speed expectations vary; simple queries may return in seconds, complex research can take minutes.

#### 🗂 Document Characteristics and Challenges
40% of documents are scanned copies with heavy tables and technical diagrams. Rich metadata like abstracts and symbols exist but vary between documents. Complex hierarchical structures and cross-document references complicate chunking and indexing. Visual content (images, formulas, graphs) requires multimodal understanding via ___Vision Language Models (VLMs)___. Symbols and domain terminologies (e.g., NASA’s 18,000+ terms) must be incorporated for semantic accuracy. The documents are mostly local, classified or unclassified but sensitive, and not cloud-hosted. On-premise deployment preferred, but initial development uses cloud and hybrid models.

#### ⚙ Document Processing Pipeline
Use ___IBM’s DockLing___ for document parsing: detects tables, figures, formulas, text, and document hierarchy. Tables are extracted as images and textual representations; complex tables require special handling. Formulas detected and cropped as images for VLM-based interpretation. Images and diagrams processed with VLMs to generate descriptions and contextual metadata. Metadata extraction (abstracts, titles, symbols) is leveraged to improve search relevance. Chunking strategy incorporates document hierarchy and adjacent context to maintain semantic coherence. Pipeline designed for extensibility and iterative improvement based on user feedback.

#### 🤖 AI Model Integration and Challenges
Initial experiments with OpenAI GPT, Claude, and open-source models like Quen and Gemini for text and VLM tasks. Challenges include API rate limits, model hallucinations, token limits, and response inconsistencies. JSON and Markdown outputs explored for table extraction; Markdown preferred for flexibility despite minor formatting issues. Confidence scoring proposed at multiple levels (pre-processing, agent response) to flag uncertain or low-quality results for review. Iterative approach to model selection and prompt engineering to balance accuracy, cost, and speed. Emphasis on building a generalized system that imitates human domain intuition without overfitting prompts.

#### 🛠 Development and Next Steps
Live coding sessions involve extensive debugging, model testing, and pipeline tuning. Focus on completing document processing (tables, formulas, images) before advancing to agent design and deployment. Planned future work: improve complex table extraction, optimize formula detection, implement hierarchical chunking, and build confidence scoring. System will be open-sourced with detailed documentation and test cases. Continuous domain learning through conversations with experts and iterative user feedback integration.

### Summary of Video Content: Building a Scalable RAG System for Complex Aerospace Documents
##### Introduction and Project Overview
[00:22 ~ 03:49]
Raj introduces himself as an AI engineer with experience building AI agents and RAG (Retrieval-Augmented Generation) systems, especially for regulated enterprises such as pharmaceutical companies and banks. The focus of this live stream is to build a RAG system that handles complex aerospace documentation, particularly rocket science documents from NASA. The initial scale is 10,000 documents, with plans to scale to 85,000+ documents.
The documents contain complex technical content including diagrams, formulas, scanned copies, tables, and regulatory filings. The goal is to build a system capable of understanding and retrieving information from these documents, including mathematical equations and technical diagrams, at scale. Raj emphasizes a raw, fresh approach, sharing his thought process and practical coding live.
##### Use Case: Meridian Aerospace
[03:50 ~ 10:30]
Raj presents a fictional but realistic use case based on Meridian Aerospace, a midsize aerospace engineering consultancy with 180 employees. Over 25 years, they accumulated approximately 85,000 documents, including propulsion test reports, safety analyses, failure investigations, specifications, and compliance filings dating back to the 1990s.
Challenges include heavy use of scanned documents (40%), complex technical jargon, mathematical formulas, and structural cross-references across documents. Engineers spend 4-6 hours per project searching archives for critical historical data, institutional knowledge is locked in retiring senior engineers’ minds, and missed information has led to failures in safety reviews.
The documents are mostly local, classified or unclassified but sensitive, and not cloud-hosted. The system must work primarily on-premise but will use a hybrid approach with cloud and open-source models for prototyping. Key requirements include semantic search that understands technical diagrams, equations, and domain-specific language, with minimal assumptions and high accuracy.
##### Domain Understanding and Initial AI Assistance
[11:21 ~ 25:12]
Raj uses Claude (an AI assistant) to better understand the aerospace domain and the specific needs of the system. Claude summarizes the core problem as a knowledge management and enterprise search challenge, highlighting the inadequacy of keyword search and the need for semantic search with vector databases and multimodal embeddings.
Technical difficulties include handling scanned PDFs without OCR reliance, extracting and embedding domain-specific terminology (NASA has over 18,000 domain terms), and interpreting diagrams and formulas. Raj plans to embed terminology vocabularies and use domain-adapted embeddings or leverage model fine-tuning with domain knowledge.
He stresses the importance of building an agent that thinks like a domain expert (engineer/scientist), recognizing the user’s personality and search behavior. The system should be flexible, dynamic, and able to clarify ambiguous queries rather than making assumptions. Measuring confidence in results and transparency of sources is critical.
##### User Personas and Success Criteria
[25:13 ~ 45:42]
Raj defines two user personas:
Sandra – a 52-year-old senior engineer with 25 years at Meridian Aerospace. She is very experienced, comfortable with command lines, values exact specifications, and wants to validate her mental model. She expects highly accurate, non-vague results and efficient knowledge transfer to junior engineers.
Junior Engineer – a 28-year-old with 3 years experience, tech-savvy and eager to learn but with high expectations for proactive search assistance. He expects the system to understand incomplete or inaccurate queries and help him avoid repetitive questions to seniors.
Success means the system finds the right documents reliably, avoids false positives, provides source transparency, and integrates confidence scoring. Speed is important, but complex queries can take minutes, which is acceptable given the time saved overall. The system should support iterative refinement of queries and follow references across documents.
##### Document Characteristics and Initial Data Collection
[45:43 ~ 01:37:55]
Raj spends significant time exploring and visually reviewing the NASA documents to understand their nature and complexity. The documents are very diverse: some are clean PDFs, others scanned, many contain tables, graphs, images, formulas, and handwritten notes.
Tables are large and complex, often spanning multiple pages with nested groupings and embedded visual elements. Diagrams and graphs are numerous and intricate. Abstracts and metadata are sometimes present, which can be used to improve indexing. Symbols used in formulas and documents are standardized and important for accurate interpretation.
Raj highlights the need for hierarchical chunking of documents to respect sections and sub-sections, rather than naive chunking. The goal is to preserve document structure and context for better retrieval and comprehension by the AI.
##### Technology Stack and Pipeline Planning
[01:37:56 ~ 02:24:00]
Raj plans to use Dockling (an IBM tool) for document parsing, which supports PDF, DOC, PPTX formats and provides table detection, text extraction, and document layout understanding. Dockling will be used as the base for parsing documents into structured chunks with metadata.
Quadrant will be used for vector storage and indexing, with open-source or cloud-hosted multimodal models (such as Together AI’s Quen) for embeddings and visual understanding.
He emphasizes a phased approach:
Phase 1: Document processing foundation (table, formula, image extraction)
Phase 2: Embedding setup and vector store integration
Phase 3: Agent and RAG system development
Raj will initially process 10,000 documents from NASA, pulled via API with rate limits, and stored locally for offline processing.
##### Document Processing: Table Extraction
[02:24:01 ~ 04:20:58]
Raj demonstrates code and pipeline for extracting tables from the documents using Dockling. Tables are detected and extracted as images and text. Due to the complexity and noisiness of tables (e.g., multi-page vertical tables, merged cells, footnotes), Raj suggests sending both the image and extracted text to a Visual Language Model (VLM) to generate JSON or markdown representations along with notes on nuances that text alone cannot capture.
He tests different Dockling models and parameters to improve table detection accuracy, including cell matching options and bounding boxes for table regions. Some tables are missed or partially extracted, highlighting the complexity of aerospace documents.
Raj runs the extracted tables through VLMs (Together AI’s Quen, Alibaba Cloud, and Claude) to generate structured markdown tables and notes, dealing with API rate limits and model timeouts. He finds markdown output more practical than JSON due to JSON’s strictness and error-proneness.
He acknowledges that 90-95% accuracy is achievable, but some complex tables may require manual or custom post-processing. Confidence scoring and fallbacks to displaying original table images are also suggested for user verification.
##### Formula Extraction
[04:20:59 ~ 06:59:41]
Raj proceeds to formula extraction, a critical aspect due to the technical nature of aerospace documents. Dockling’s layout detection is used to locate formulas, cropping them as images for VLM interpretation.
The formula extraction pipeline uses similar principles to tables: detect formulas, crop images, send to VLM for LaTeX or markdown conversion with notes.
Initial results show some formulas are accurately extracted, but many are missed or hallucinated. Raj discusses padding and cropping adjustments to improve formula capture.
He suggests a fallback where entire pages containing formulas are sent to the model to ensure no formula is missed, prioritizing accuracy over efficiency.
Raj compares outputs from different VLM models (Claude, Together AI’s Quen), finding Claude more accurate on complex formulas.
The pipeline includes capturing standardized symbols and notation, which are crucial for interpreting formulas correctly across documents.
##### General Observations and Next Steps
##### [06:59:42 ~ 07:07:53]
Raj reflects on the complexity and time required for accurate document processing at this scale and domain complexity. He stresses the importance of iterative testing, human-in-the-loop evaluation, and continuous refinement of preprocessing and AI prompting.
The development plan includes completing table and formula extraction, followed by image/diagram processing and hierarchical chunking.
Confidence scoring, error handling, and source transparency are critical to building user trust in the system.
Raj plans to share the GitHub repository and continue development in future live streams, emphasizing that the current work is a foundational prototype to be improved upon.
He advises others to spend significant time understanding domain documents and user needs before jumping into coding large-scale AI document processing systems.
##### Key Insights and Takeaways
Building a production-grade RAG system for aerospace documents requires deep domain understanding, extensive data exploration, and sophisticated document parsing strategies.
Complex aerospace documents combine scanned materials, technical jargon, formulas, intricate tables, and diagrams, making naive document chunking or keyword search ineffective.
Using Dockling for document layout parsing combined with VLMs for multimodal understanding (text + images + formulas) helps extract meaningful structured data.
Semantic search must handle domain-specific terminologies and provide high accuracy with minimal assumptions, supported by confidence scores and user feedback loops.
User personas highlight the need for precision, transparency, iterative refinement, and source referencing; the system must respect domain experts’ workflows.
Real-world deployment requires hybrid cloud and on-premise solutions, handling sensitive data and scaling to tens of thousands of documents.
API limitations and model selection impact processing speed and accuracy; batching and local inference are important considerations.
Tables and formulas are the most challenging extraction tasks and often require custom handling, fallback strategies, and hybrid text/image processing.
Iterative development, testing with domain experts, and flexible architecture are essential for success in such specialized AI systems.


#### FAQ
Q: Why is naive keyword search insufficient for aerospace documents?
A: Because aerospace documents contain domain-specific jargon, scanned images, complex tables, and formulas, keyword search fails to find semantically relevant information buried in historical or unstructured data.

Q: What role does Dockling play in this system?
A: Dockling is used for document layout parsing, detecting tables, formulas, images, and extracting text chunks with metadata, serving as the foundation for structured document understanding.

Q: How are complex tables processed?
A: Tables are extracted as images and text, then sent to Visual Language Models for markdown or JSON conversion with notes capturing nuances that text alone cannot represent.

Q: What challenges exist in formula extraction?
A: Formulas are often cropped images; extracting them requires accurate detection, cropping, and interpretation by VLMs, with fallback to sending entire pages to ensure no formula is missed.

Q: How is user trust ensured in AI-generated answers?
A: Through confidence scores, transparent sourcing, iterative query refinement, and an interface that allows users to verify results against original documents and images.

Q: Can this system be fully cloud-based?
A: While the prototype uses cloud and open AI models, the system is designed to support on-premise deployment for regulated enterprises with sensitive data.

This summary comprehensively captures the video’s content, reflecting the detailed walkthrough, architectural planning, technical challenges, and AI strategies involved in building a scalable RAG system for complex aerospace documents.

### Keywords
RAG (Retrieval-Augmented Generation)
Aerospace Documents
Semantic Search
Multimodal AI (VLM)
Document Parsing
Dockling
Vector Database (Quadrant)
Domain Terminology Embeddings
Confidence Scoring
Table Extraction
Formula Extraction
On-Premise AI Deployment
NASA Documents
AI Agent Design
Domain Expert Personas
