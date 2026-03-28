
## [Building Production RAG for 10K+ NASA Docs (Scales to 85K+): Rocket Schematics and more! | Part 1 ](https://www.youtube.com/live/bkKVWf7qQUk?si=YL2UrWcjZH18B9SZ)
### Outline of the Video Content
1. Introduction: Background and Project Scope
2. Use Case Description: Meridian Aerospace and Data Challenges
3. Domain Exploration: AI-Assisted Understanding with Claude
4. User Personas and System Success Criteria
5. Document Characteristics and Visual Exploration
6. Technology Stack: Dockling, Vector DB, VLMs, and Phased Development
7. Document Processing: Table Detection and Extraction
8. Table Representation: Markdown vs JSON, Image Support, and Model Comparisons
9. Formula Extraction: Cropping, VLM Processing, Challenges, and Solutions
10. General Observations: Confidence Scoring, Evaluation, and Next Steps
11. Wrap-Up: Future Work and Repository Sharing

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



## [Table Extraction, Formulas & VLM Pipeline| Building for 10K→85K Documents | NASA RAG | Part 2](https://www.youtube.com/live/ozYl0MiM74A?si=zKQjTtZrE4kykQHU)

### Outline of the System Pipeline and Workflow

1. **Document Ingestion**
   - Accept scanned PDFs and digital documents.
   - Convert pages to images as needed.
2. **Layout Detection**
   - Use Dockling or similar open-source tools to detect text blocks, tables, figures, formulas.
   - Extract bounding boxes and reading order metadata.
3. **Table Processing**
   - Apply pixel-level heat map and boundary detection.
   - Draw horizontal boundary lines and zebra striping.
   - Two-pass chunking with header extraction, processing smaller column groups.
   - If confidence low, fallback to detailed textual description.
4. **Figure/Image Processing**
   - Detect figure bounding boxes.
   - Crop images with padding.
   - Extract surrounding contextual text (above and below).
   - Classify figure types and filter out non-technical noise.
5. **Formula Processing**
   - Detect formulas using layout detection.
   - Process entire pages containing formulas with VLMs.
   - Extract formula text and surrounding explanatory text in order.
6. **Symbol Extraction**
   - Use semantic search to identify symbol sections.
   - Extract symbol definitions from identified pages (typically 1-3 pages).
   - Normalize inconsistent naming (symbols, abbreviations, variables).
7. **Metadata Extraction**
   - Detect report documentation pages using regex (e.g., NASA SF 295).
   - Extract report number, title, author, abstract, document type.
   - Use metadata for enhanced document sorting and filtering.
8. **Chunking and Ordering**
   - Combine all extracted content into ordered chunks based on bounding boxes and reading order.
   - Include metadata and chunk-specific tags.
   - Store chunks in vector database or document store for downstream retrieval.
9. **Search and Agent Integration**
   - Use extracted metadata and chunk content to build domain-aware search.
   - Integrate with AI agents for reasoning over complex documents.



#### [00:00:20 ~ 00:04:17] Introduction and Context of the Project
The speaker welcomes viewers to the second part of a series focused on building an AI system tailored for processing complex rocket science and aerospace documents. The goal is to build an on-premises AI system capable of handling over 85,000 classified and unclassified technical documents, many containing dense technical diagrams, mathematical formulas, scanned copies from the 1970s, and modern documents. The previous video covered initial document processing, solving formulas, and basic text extraction but struggled with accurately processing tables. The current session is dedicated to tackling the table extraction problem, especially on challenging documents like a scanned 1967 rocket science document. The problem involves working with scanned images (not clean PDFs), with no access to raw text, requiring innovative AI methods to extract table data. OpenAI’s GPT-like models can extract tables well but due to cost and privacy concerns, the aim is to use open-source vision-language models (VLMs), which are prone to hallucinations and errors. The speaker outlines a plan to first focus on table extraction, then move to images, graphs, and domain terminologies, eventually integrating all into an AI agent.

#### [00:04:17 ~ 00:11:46] Challenges and Creative Approaches to Table Processing
Simple tables from modern PDFs are solvable using existing tools like Quen, which output accurate markdown representations. The 1967 scanned document table is complex: 18 rows and around 50 columns, with many intricacies and noise. VLMs hallucinate heavily on such tables, misreading dashes or numbers, causing inaccurate outputs. Humans use rulers to align and read complex tables; the speaker aims to mimic this process algorithmically. To tackle this, the speaker developed a heat map approach based on pixel-level analysis of the table images. By analyzing black and white pixels, the algorithm identifies gaps (white space) between columns and rows, which act as natural boundaries. Horizontal “projectile lines” or boundary lines are drawn over the table image to segment it visually, with zebra striping (alternating row colors) to help AI models focus and reduce confusion.  This visual overlay acts as a kind of “ruler” mimicry, helping the AI better parse the table structure. Although this method improves accuracy, hallucinations remain due to complexity and noise. To mitigate this, a two-pass approach is used: 
  - First pass extracts fixed headers using VLM.
  - Second pass processes segmented chunks of the table with known column headers to reduce confusion.
This chunking allows the model to focus on smaller segments (e.g., four columns at a time) rather than the entire 50-column table. Despite these efforts, challenges remain, especially with non-uniform tables containing arrows, missing numbers, and inconsistent formatting. The speaker acknowledges the method works about 80% of the time and invites others to build upon this creative baseline.


#### [00:11:46 ~ 00:22:43] Limitations and Future Directions for Table Extraction
The speaker reflects on the limitations of horizontal parsing due to mixed content like arrows and irregular column patterns. Vertical parsing was considered but found impractical because of irregular column spans and mixed content. The need for a stable, generalizable table extraction approach remains. Potential future solution: train a neural network for layout detection and table segmentation using thousands of annotated samples.  However, generating accurate training data is expensive and error-prone with open-source models. The speaker suggests heat maps, boundary detection, and layout analysis as promising but currently incomplete approaches. Emphasizes the importance of creativity and experimentation in this domain, since there are no established rule books for VLM-based table extraction. Notes that even large-funded commercial tools struggle with complex tables, motivating the need for custom solutions. Mentions other tools like Llama-Cloud and Landing AI but prefers open-source approaches integrated into their workflow. The speaker plans to generate rich textual descriptions of complex tables to supplement imperfect table extraction. The system will flag complex tables and fallback to descriptive summaries if accurate markdown extraction fails. This approach balances accuracy and token efficiency by avoiding per-cell processing (which would require thousands of API calls and be inefficient).

#### [00:22:43 ~ 00:37:16] Interactions with OpenAI Models and Refining the Pipeline
The speaker experiments with prompting strategies to guide the VLM to classify tables as simple or complex. For complex tables, the model outputs detailed textual descriptions rather than markdown extractions. This reduces hallucinations and token waste on complicated layouts. The new approach removes inefficient cell-by-cell processing. The speaker emphasizes an iterative approach: get a robust foundation first, then improve with finer tuning later. Testing with real-world scanned documents from NASA confirms the pipeline works well on clean and moderately complex tables. Metadata such as page numbers and bounding boxes are extracted to organize and contextualize table chunks. Some inconsistencies remain due to rotated images or portrait vs landscape layouts. The speaker decides not to rotate or transform bounding boxes in production to avoid introducing errors. The goal is to reliably detect all tables, including missing or continued tables, and maintain consistent chunk order. The speaker also discusses multi-page tables and how to handle them properly with metadata. The approach will be integrated into a unified pipeline that processes formulas, images, tables, and symbols in a single pass.

#### [00:37:16 ~ 01:00:32] Figures, Images, and Noise Filtering
Next focus is on detecting and extracting figures, images, diagrams, and their captions. Dockling’s figure detection capabilities are used to extract bounding boxes of figures. Instead of sending entire page images, the system crops figures with some padding and extracts surrounding contextual text (above and below) for improved understanding. The system classifies figures into types: graphs, semantic diagrams, flowcharts, photos, etc.  A major challenge is noise filtering: many documents contain irrelevant artifacts like confidential stamps, logos, page numbers, and other non-technical marks. The speaker plans to have the AI classify images as technical or non-technical (document artifacts). Non-technical figures will be marked as irrelevant to avoid polluting the search index. Testing shows the approach extracts figures and descriptions with high accuracy, improving search relevance. Padding around images is adjusted to ensure that captions and nearby text are included without excessive noise. The speaker stresses the importance of visually clean and semantically rich figure extraction for downstream tasks. The approach is designed to be generic and scalable, supporting thousands of documents with varied image content.

#### [01:00:32 ~ 01:32:00] Domain Terminologies, Symbols Extraction, and Document Metadata
Symbols are crucial to rocket science documents as they define variables and domain-specific notations. The system detects symbol sections which typically appear in 1-3 pages, often near the beginning or end of documents. A two-pass approach is used: 
  - First pass performs semantic or keyword search to identify symbol-related chunks.
  - Second pass extracts and synthesizes symbol definitions using a VLM.
The speaker notes variability in how symbols are labeled across documents (symbols, abbreviations, variables), requiring flexible semantic search rather than strict keyword matching. The system also extracts report metadata from “report documentation pages” (e.g., NASA’s Standard Form 295). These pages contain valuable metadata like report number, title, authors, abstract, and document type (e.g., technical memorandum, contractor report). The speaker explains that these metadata pages are typically standardized across NASA and DoD reports, but private companies like SpaceX or Boeing may use proprietary formats. Regex and pattern matching are used to identify and extract metadata pages from scanned documents. This metadata enables advanced search filtering, such as finding all technical memorandums from a certain year or author. The speaker emphasizes that metadata extraction is essential for large-scale document management and user-centric search. The system avoids relying on PDF metadata which can be inaccurate or missing, especially in scanned historical documents. Abstracts are highlighted as valuable because they provide concise summaries written by original authors, serving as reliable search entry points. The speaker plans to integrate symbols, metadata, tables, formulas, images, and chunking into a single, efficient pipeline for document ingestion.


#### [01:32:00 ~ 02:00:00] Pipeline Integration, Chunking, and Order Preservation
The speaker discusses merging multiple extraction components (tables, formulas, figures, symbols, metadata) into one coherent processing pipeline. Maintaining the correct reading order of document content is critical for accurate context and retrieval. Dockling’s layout detection provides bounding boxes and item ordering, which the system leverages to reconstruct reading order. Bounding boxes and vertical positions help sort extracted elements on a page, especially when multiple tables, images, or formulas coexist. The speaker rejects overcomplicated sorting mechanisms in favor of simpler bounding box-based sorting to avoid bugs and maintain efficiency. Formulas are challenging because dockling often misses or partially extracts them. To ensure formula accuracy, the system sends entire pages containing formulas to a VLM for thorough processing, prioritizing accuracy over efficiency. The speaker contemplates placeholder-based formula chunking but finds it complex and error-prone. Instead, they propose chunking full pages with formulas and prompting the LLM to extract formulas and surrounding text in proper order. This method balances cost and accuracy: formula-heavy pages are a minority and can be handled with more compute resources. The speaker also discusses the challenges of maintaining semantic coherence across chunks, especially for formulas that span multiple lines or pages. Chunk size and token limits are considered in pipeline design to optimize API calls without sacrificing data fidelity. The system is designed for parallel processing of thousands of documents overnight, scalable with GPU infrastructure. The speaker highlights the iterative, experimental nature of the project, emphasizing continuous improvement and validation.

#### [02:00:00 ~ 02:45:00] Testing, Validation, and Performance
The system is tested on various NASA documents with complex tables, images, formulas, and symbols. Extraction accuracy is manually verified for tables, figures, and symbols. The system successfully extracts multiple tables, including multi-page and continuation tables. Figures and images are extracted with captions and classified by type. Symbols and abbreviations are detected but require semantic search improvements for robustness. The pipeline runs on a Mac CPU with no GPU acceleration, leading to longer processing times (40-50 seconds per document). GPU acceleration is expected to reduce processing times by at least 50%, improving throughput.  Batch processing and model loading optimizations are planned to further enhance speed and reduce overhead. The speaker notes some import and runtime issues in the code but considers them minor and fixable. Overall, the system achieves a good balance between extraction accuracy, processing speed, and scalability. The speaker stresses the importance of solid, reliable chunking and metadata extraction before moving on to agent design and advanced search features.

#### [02:45:00 ~ 04:00:00] Remarks on Domain Specificity and Practical Considerations
The system is specialized for aerospace/rocket science documents, leveraging domain knowledge such as NASA’s document standards. This domain-specific approach enables more accurate metadata extraction and search capabilities. The speaker cautions against applying this exact system to unrelated domains like finance without adaptation. They emphasize building domain-specific heuristics, regex patterns, and chunking logic tailored to document conventions. The system supports open-source AI models, running fully on-premises for security and compliance. This makes it suitable for sensitive industries like banking, pharmaceuticals, and defense. The speaker highlights the business value of accurate table extraction and metadata in aerospace research, noting it as a large market opportunity. The final goal is to develop a unified pipeline that processes all document elements (text, tables, images, formulas, symbols, metadata) accurately and efficiently. This foundational work will enable building intelligent agents that understand and reason over complex technical documents. The speaker invites viewers to explore the open-source codebase and experiment with the creative approaches demonstrated.

### Key Insights

- **Table extraction from scanned complex technical documents is highly challenging** due to noise, irregular layouts, and mixed content like arrows and formulas.
- **Pixel-level heat map and boundary detection combined with zebra striping help VLMs better parse tables** by mimicking human ruler-based reading.
- **Two-pass chunking approaches reduce hallucinations by narrowing VLM focus to smaller segments with known headers.**
- **Fallback to descriptive summaries for complex tables balances accuracy and token efficiency.**
- **Figure/image extraction must include surrounding contextual text and classify technical vs non-technical content to avoid noise.**
- **Symbol extraction relies on semantic search rather than strict keyword matching due to inconsistent labeling.**
- **Metadata extraction from standardized report documentation pages (e.g., NASA SF 295) enables powerful filtering and search.**
- **Maintaining reading order via bounding box sorting is critical for coherent chunking across mixed content types.**
- **Formulas require special handling: entire pages are processed by VLMs to ensure completeness and accuracy.**
- **The system prioritizes accuracy over efficiency for formulas and complex tables, leveraging local GPU compute.**
- **Domain specificity (aerospace) enables use of standard document structures and metadata conventions, improving extraction.**
- **The project demonstrates a novel, fully on-premises AI pipeline for complex technical document understanding at scale.**



### FAQ

**Q: Why is table extraction so difficult in rocket science documents?**  
A: These documents often come as scanned images with noisy layouts, mixed content like arrows and formulas, inconsistent column spans, and no clean text. Open-source VLMs hallucinate or misinterpret these complex patterns, making extraction challenging.

**Q: How does the heat map and boundary detection help?**  
A: It mimics how humans read tables using rulers by detecting pixel-level gaps between rows and columns, drawing horizontal boundary lines and zebra stripes to visually segment the table. This helps VLMs focus on structured parts rather than generalizing the entire table at once.

**Q: What is the fallback when table extraction is too complex?**  
A: Instead of forcing a markdown extraction, the system outputs a detailed textual description that captures key information and nuances, which is then chunked for search and retrieval.

**Q: How are figures and images processed?**  
A: Figures are detected with bounding boxes, cropped with padding, and surrounding contextual text is extracted to provide semantic context. The system classifies figures into types and filters out non-technical noise like logos or stamps.

**Q: How does the system handle symbols?**  
A: Symbols are extracted by identifying symbol-related chunks via semantic search, then synthesizing symbol definitions from typically 1-3 pages. This accommodates variability in labeling (symbols, abbreviations, variables).

**Q: What metadata is extracted and why is it important?**  
A: Metadata such as report number, title, author, abstract, and document type (e.g., NASA technical memorandum) is extracted from standard report documentation pages. This enables powerful filtering, sorting, and search capabilities across tens of thousands of documents.

**Q: How is reading order maintained during chunking?**  
A: The system uses layout detection bounding boxes and vertical positioning to sort extracted items, preserving the logical reading order across text, tables, images, and formulas.

**Q: Why are formulas processed differently?**  
A: Formula extraction is error-prone with current models. The system processes entire pages containing formulas with VLMs to ensure accuracy, prioritizing correctness over token efficiency.

**Q: Can this system be used in other domains?**  
A: The system is highly domain-specific, optimized for aerospace/rocket science documents with known conventions. Applying it directly to other domains like finance would require significant adaptation.


## [Formula Extraction, Visual Anchoring and more for NASA docs from 1960s | NASA RAG | Part 3 ](https://www.youtube.com/live/1do7SXZ12dk?si=sKqO8D4GCLNLtknB)
### Key Insights and Takeaways
- **Formula Extraction is a Major Bottleneck:** Accurate formula extraction demands 100% precision, requiring innovative visual bounding box approaches combined with VLMs to maintain spatial context and ordering.
- **Bounding Box Visualization Enhances Model Understanding:** Annotating document images with numbered bounding boxes around paragraphs allows the VLM to associate formulas correctly, preserving reading order and meaning.
- **Prompt Engineering Balances Complexity and Model Reasoning:** Providing the model with clear but minimal instructions enables it to leverage its training to handle complex chunking and inline formulas.
- **Noise Filtering and Visual Clarity Are Crucial:** Removing irrelevant small bounding boxes and using alternating colors for boxes help prevent model confusion and improve chunk ordering.
- **Integration into a Unified Chunking Pipeline:** Text, formulas, images, and tables are chunked via separate pipelines but integrated via bounding box ordering and metadata to maintain document coherence.
- **Embedding and Metadata Enrichment for Retrieval:** Using open-source embedding models with rich metadata inclusion enables efficient and accurate semantic search over complex aerospace documents.
- **Infrastructure and Cost Considerations:** Efficient batching, parallelization, and selection of model sizes balance accuracy and compute cost, enabling processing of 10k+ documents within practical timeframes.
- **Agent Layer for Final Verification and Reasoning:** Remaining edge cases and accuracy gaps can be mitigated by an agent layer that cross-validates formulas and context through visual and textual analysis.
- **Engineering Mindset:** Deep understanding of code, creative problem-solving, and leveraging AI tools effectively are key to building robust domain-specific RAG systems.

#### [00:00:12 ~ 00:02:44] Introduction and Project Overview  
The presenter welcomes viewers to the third day of building a Retrieval-Augmented Generation (RAG) system targeting a NASA-like aerospace consulting company, Meridian Aerospace. This fictional company manages 85,000+ technical documents spanning decades (1960s to present), including formulas, images, graphs, diagrams, and technical jargon-heavy content. The project’s goal is to process and index these documents efficiently to enable accurate retrieval and question answering over complex aerospace data. The first two days involved research, conversations with Claude (an AI assistant), and significant progress in processing different document types, especially handling complex tables, images, and diagrams. The presenter encourages viewers to review previous sessions for background and notes that 90% of document processing is complete.

#### [00:02:17 ~ 00:08:42] Challenge of Formula Extraction and Initial Solutions  
Formulas present a unique challenge because they must be extracted with 100% accuracy, preserving their exact structure and meaning. The team initially used an IBM model called Dockling to extract formulas from documents. However, Dockling only partially extracts formulas on a page and misses many, which is unacceptable given the critical nature of aerospace formulas. The approach was changed to pass entire page images to a vision-language model (VLM) to extract formulas accurately.  
However, processing entire pages sacrifices the ability to associate formulas precisely with their corresponding text paragraphs, since bounding box data (which gives the location of text elements) is lost when passing whole pages. This disrupts the logical ordering of text and formulas, leading to meaning loss. For example, a formula directly linked to a preceding text paragraph should not be separated or misplaced, as this confuses downstream language models.  
An inefficient workaround involved chunking formulas separately and associating them with text, but this was costly in compute and token usage when many formulas appeared densely in documents.  


#### [00:08:47 ~ 00:17:33] Innovative Bounding Box Visualization Approach  
To address the spatial ordering problem, the presenter proposes a novel solution leveraging bounding boxes from Dockling to draw visual numbered boxes around each paragraph or text chunk on the document image. Each paragraph is given a unique number (box 1, box 2, etc.), visually marked with colored borders. The image with these numbered boxes is sent to the VLM, which is then prompted to identify which formulas belong under which numbered box.  
This approach retains spatial context, enabling the model to output formulas associated with the correct paragraph without losing ordering. The model can output formula arrays tagged with box IDs, maintaining formula order and adjacency to text. This technique promises 100% accuracy in formula placement because the bounding boxes provide explicit positional cues.  
The presenter notes that this works even if formulas are isolated without nearby text (since formulas themselves have bounding boxes). They acknowledge edge cases like dense formula-only pages but believe the model's ordered output will handle them well.  
The plan includes first generating these annotated images with numbered bounding boxes, then sending them to the VLM for formula extraction and association. This is more efficient than processing formulas and text separately and leverages visual context to maintain document structure.

#### [00:17:33 ~ 00:36:57] Implementation Details and Prompting Strategies  
The presenter interacts with Claude, verifying the approach and revoking previous inefficient code. They emphasize the importance of using dark, visible colors (red, dark blue) for bounding boxes and numbers to ensure good visual contrast for the model. Light colors are avoided as they may be missed.  
They discuss how the VLM should be prompted to output formulas in reading order, associating each with the correct box. The model will receive images with numbered boxes and return JSON mapping formulas to boxes. The approach can also handle inline formulas embedded within paragraphs by labeling box ranges (e.g., start box 7 to end box 8), allowing chunking of text with inline math.  
They acknowledge complex edge cases where formulas and text are mixed intricately, requiring the model to intelligently group formulas and inline math within paragraph boundaries. Multiple prompt versions are discussed for handling standalone formulas versus inline math regions.  
The presenter tests the approach on various pages, including scanned documents and PowerPoint-like slides with complex layouts, noting limitations and the need to treat large figures or diagrams as single chunks. They iterate on prompt design and bounding box handling to improve accuracy and visual clarity.  
They conclude that the bounding box visualization approach combined with VLM extraction is the most accurate and efficient method to date, solving a major bottleneck in formula extraction for complex technical aerospace documents.


#### [00:36:57 ~ 02:02:37] Handling Complex Inline Formulas and Chunking Logic  
The presenter dives deeper into handling inline formulas mixed with text, a challenging edge case. They explore strategies to process bounding box ranges to include both text and embedded formulas cohesively, avoiding fragmented or inaccurate chunks.  
They discuss different chunking options:  
- Chunking paragraphs with embedded formulas as a single unit (recommended).  
- Replacing inline formulas with references (formula IDs) to avoid duplication.  
- Accepting some duplication but managing it downstream.  
They emphasize that the model should not be overburdened with complicated instructions but should rely on its reasoning capabilities to group text and inline math properly.  
The presenter also suggests using visualizations like markdown diagrams to better understand and communicate chunking and formula placement strategies.  
They decide to send the entire page image with bounding boxes to the model and let it figure out the best chunk boundaries, rather than processing region-by-region to avoid losing context in overlapping or connected formulas.  
They also discuss post-processing steps to merge or deduplicate formula chunks and inline math to produce coherent final chunks.  
The overall emphasis is on balancing complexity, accuracy, and efficiency while leveraging the VLM’s visual reasoning to maintain document integrity.


#### [02:02:37 ~ 03:11:09] Ordering of Formulas and Integration into Unified Chunking Pipeline  
After solving formula extraction and placement, the team focuses on ordering the formulas correctly within the document flow. They want to insert formula chunks in the right order following adjacent text paragraphs, preserving natural document reading order.  
They review their current pipeline and confirm progress on integrating formula extraction results into the unified chunking system alongside text, tables, and images.  
Challenges include:  
- Maintaining order across multiple pages with multiple bounding boxes per page.  
- Handling page headers or other non-content elements that may affect bounding box numbering.  
- Sorting chunks by page number and bounding box position.  
They discuss filtering out noise and irrelevant chunks, especially very small bounding boxes or symbols that do not contribute to meaningful content.  
They explore different approaches to numbering chunks:  
- Iterating over all items (text, images, formulas) and numbering accordingly.  
- Filtering only text items for chunk numbering and handling images/formulas separately.  
They decide to keep all items numbered to maintain spatial coherence and avoid losing ordering when images or formulas appear between paragraphs.  
They note that the chunker should only chunk text regions and rely on separate pipelines for formulas, tables, and images to maintain modularity.  
They also consider the impact of overlapping bounding boxes and inline formulas on chunk boundaries and ordering, emphasizing the need for visual clarity in bounding box annotation to avoid misinterpretation by the model.

#### [03:11:09 ~ 06:04:00] Visual Improvements, Noise Filtering, and Model Prompt Refinement  
The presenter makes further improvements to the visual representation of bounding boxes on document images:  
- Adjusting box number placements to avoid overlap with text.  
- Using alternating colors (red and blue) for boxes to distinguish adjacent chunks clearly.  
- Filtering out very small or irrelevant bounding boxes (noise) such as dots or stray marks using minimum width/height thresholds in Dockling’s layout detection.  
- Encouraging the model to use domain intuition and training to intelligently group small boxes that are part of larger paragraphs (e.g., small inline formulas inside a larger text box).  
They discuss the trade-offs between using a reasoning VLM model versus a non-reasoning model, deciding to keep the prompt simple and let the model’s training handle chunking decisions. Reasoning models may overthink or delay responses.  
Prompt engineering focuses on instructing the model to associate formulas with appropriate bounding boxes and output ordered chunks without overcomplicating instructions.  
The presenter also tests multiple documents, including older scanned PDFs (from the 1950s to 1980s), achieving 90–95% accuracy on formula extraction and chunking despite challenging layouts.  
They acknowledge some remaining edge cases requiring agent-level verification: e.g., verifying formulas near chunk boundaries by passing images of adjacent bounding boxes to the agent for confirmation.  
Overall, the system achieves high accuracy for complex aerospace documents using open-source models and custom pipelines.

#### [06:04:00 ~ 08:18:54] Final Pipeline Status, Chunking Strategies, and Metadata Inclusion  
The team finalizes the chunking pipeline by:  
- Ensuring noise filtering removes irrelevant chunks.  
- Setting minimum chunk sizes (e.g., merging very small text chunks below a threshold with adjacent chunks) to avoid fragmentation.  
- Maintaining paragraph boundaries with clear newlines when merging chunks to preserve document semantics.  
- Confirming that chunking is paragraph-based, avoiding overlapping chunks.  
- Including metadata such as section headers, figure types, formula IDs, notes, and key elements in chunk metadata for richer indexing and search.  
They discuss embedding models, selecting open-source contextual re-ranker models with 4–8 billion parameters quantized to 8-bit for resource efficiency. These models handle jargon and multilingual content well.  
Embedding chunk vectors will be stored in Quadrant (a vector database) for efficient retrieval.  
The presenter discusses infrastructure considerations for running embedding and VLM models on GPUs, memory requirements, token limits, parallelization strategies, and cost trade-offs (e.g., using Azure H100 or lower-end GPUs).  
They estimate processing 10,000 documents within 24 hours on a single H100 GPU with efficient batching and queuing strategies.  
They emphasize the importance of metadata for search and downstream agent reasoning, encouraging rich metadata inclusion in chunk storage.  
The presenter also shares personal reflections on engineering practices, creativity in problem-solving, and the importance of understanding code fully versus relying on auto-generated code for maintainability and debugging.

#### [08:18:54 ~ End] Next Steps and Reflections  
The project is effectively complete for the core document processing pipeline with formula extraction, chunking, bounding box visualization, and embedding integration solidly in place.  
Next steps include:  
- Finalizing embedding pipelines and metadata storage in Quadrant.  
- Building agents on top of the retrieval system to enable intelligent querying and reasoning over aerospace documents.  
- Testing with larger datasets and continuing to optimize pipelines for accuracy and performance.  
The presenter encourages viewers to explore the shared GitHub repository for the project once published and welcomes feedback and collaboration.  
They emphasize that while open-source models require significant engineering effort and custom pipelines, it is feasible to achieve near state-of-the-art performance without expensive cloud APIs.  
The session concludes with appreciation for the audience and a preview of upcoming work focused on agent design and user experience for aerospace document search.


### FAQ

**Q: Why can’t traditional text chunking handle formulas effectively?**  
A: Formulas require exact spatial and semantic context. Traditional chunking separates formulas from their adjacent explanatory text, losing meaning and causing retrieval errors.

**Q: How does bounding box visualization help formula extraction?**  
A: Numbered bounding boxes drawn around paragraphs enable the VLM to associate formulas with the correct paragraph by referencing these visual markers, preserving document flow.

**Q: What models are used for formula extraction and embedding?**  
A: An open-source VLM model processes document images with bounding boxes for formula extraction. For embeddings, quantized 4–8 billion parameter contextual re-ranker models are used.

**Q: How do you handle inline math mixed with text?**  
A: The model is prompted to output bounding box ranges covering inline math and text as a single chunk, avoiding fragmented extraction and preserving context.

**Q: What infrastructure is required for processing 10k documents?**  
A: A single high-memory GPU such as an NVIDIA H100 can process 10k documents in roughly 24 hours using efficient batching and parallel requests. Larger clusters speed this up.

**Q: How is accuracy ensured for old and scanned documents?**  
A: Accuracy is boosted by passing entire pages with bounding boxes, filtering noise, and post-processing with an agent that cross-validates formulas and adjacent context visually and textually.

**Q: Can this system be run fully on-premises?**  
A: Yes, open-source models and pipelines allow on-premises deployment with suitable GPU resources, without reliance on costly cloud APIs.


# [Building AI Agents for 10K+ Rocket Science docs from 1960s-2025s | NASA RAG | Part 4](https://www.youtube.com/live/51097p4SWkM?si=ghBZG1WMCwRcsOD5)
### Summary of Video Transcript: Building a RAG System for Aerospace Document Search (Part 4)

---

#### [00:00:09 ~ 00:10:53] Introduction and Project Recap

- The speaker welcomes viewers to part four of a series focused on building a Retrieval-Augmented Generation (RAG) system designed to work with a large corpus of aerospace documents, aiming to support up to **85,000 documents**.
- Currently, the system operates on about **10,000 documents** but is architected to scale well beyond that, potentially even to **100,000 documents**.
- The documents span a vast timeline, including highly technical papers from the **1950s through recent years**, containing formulas, tables, images, and complex jargon.
- Significant progress has been made in solving challenges around:
  - **Formula extraction**
  - **Table extraction** (including complex tables with continuations)
  - **Image understanding** and **description generation**
  - **Chunking and context extraction** for efficient document processing.
- The system uses **open-source models** from Quen (likely a reference to a model or library), including:
  - A **32 billion parameter model** for tables
  - Higher parameter Visual Language Models (VLM) for formula understanding
  - A **6 billion parameter re-ranker** running locally on a Mac, along with a **4 billion parameter embedding model** via Arama.
- The speaker emphasizes **not rushing into agent code** but first deeply understanding the **user personas, their search behaviors, and the domain problems** that the system must solve.
- The goal is to build a **specialized search and reasoning agent tailored for aerospace and rocket science documents**, not a generic search system.
- Metadata, domain knowledge, and custom retrieval techniques are key to building a solution that provides **highly relevant, domain-specific results**.

---

#### [00:14:50 ~ 00:42:42] Understanding the User and Domain Problem

- The speaker revisits conversations from earlier streams to **refresh and deepen understanding of the problem space and user needs**.
- The system is framed as an **enterprise knowledge management and AI-enhanced search system** specifically for highly technical aerospace engineering documents.
- Traditional keyword search fails in this domain because **concepts and terminology do not always match directly** (e.g., searching for "thrust chamber failure" might miss documents describing it as "combustion instability leading to chamber wall breach").
- Documents include **degraded, scanned historical files from 1950s onward**, with complex technical diagrams, formulas, and tables, all of which have been successfully processed with 90–95% accuracy using open-source models.
- Domain-specific language and acronyms are prevalent, so the system must handle **domain-specific terminology expansion and synonymy** without fine-tuning large models, instead relying on **smart retrieval and metadata**.
- The system is designed for **on-premise deployment** with all processing and indexing done locally via Docker and open-source tools, except for the agent which may use cloud-based LLMs (e.g., OpenAI Claude).
- The speaker highlights the importance of **NASA’s controlled vocabulary and thesaurus** with over 18,000 aerospace engineering terms, which will be integrated to improve retrieval.
- The typical user scenario involves engineers working on complex projects, needing **fast access to historical failure data, design specifications, and test reports** that are scattered across decades of documentation.
- Two user personas are defined:
  - **Sandra**, a senior engineer with 25 years of experience and deep domain knowledge, familiar with the document archive and searching via mental maps.
  - **Marcus**, a junior engineer, tech-savvy, adept at prompt engineering, curious, and learning the domain.
- The system must support both personas, allowing traditional keyword searches but also enabling **intelligent, reasoning-driven queries** that mimic how an expert would think.
- The speaker stresses that **speed and ease of use are critical**; queries that currently take hours should be answered in minutes, or ideally seconds.
- The system is not just a convenience tool but also a **risk mitigation and knowledge preservation platform**, ensuring **accuracy, comprehensiveness, and transparency**.
- The search process is iterative and exploratory, often requiring **following references across documents, refining queries, and integrating diverse types of information** (formulas, tables, images).
- The system must be flexible to handle **both straightforward and deep, complex search queries** with an agentic interface that reasons and proactively follows leads.

---

#### [00:45:18 ~ 01:13:25] Simulated Agent Use Cases and Reasoning Patterns

- The speaker demonstrates simulated interactions with **Claude AI** to model how an intelligent agent would reason through complex aerospace engineering queries.
- Example scenario:
  - Sandra is investigating **thermal margin issues at elevated chamber pressures** related to a past program (Europa).
  - The agent forms an initial hypothesis, then searches historical test reports, failure analyses, and design documents.
  - Upon retrieving relevant documents, the agent updates its task list, reasons about findings, and pursues leads such as injector design issues or prior test failures.
  - The agent balances **parallel and sequential task management**, deciding when to follow up on new leads or wait for critical information before proceeding.
- The agent is designed to behave like a **colleague with photographic memory** of all documents, able to synthesize scattered information into coherent, actionable insights.
- The simulation reveals key agent behaviors:
  - **Broadening search terms and strategies** to increase chances of finding relevant information.
  - Searching for **both failure and success cases** to provide balanced context.
  - Keeping a **dynamic to-do list and notes** for tracking investigation progress.
  - Avoiding hardcoded templates or rigid search patterns, instead allowing **domain intuition and adaptive reasoning**.
- The speaker emphasizes that **semantic search and retrieval alone are insufficient**; the agent must reason, analyze, and synthesize information intelligently.
- Simulations allow the designer to **discover unknown unknowns** in the domain and agent behavior, guiding system design.
- The agent’s personality and approach vary by user:
  - Sandra’s mindset is exhaustive, wide-net, pattern-finding across decades.
  - Marcus’s mindset is hypothesis-driven, focused on quickly testing specific leads.
- The system prompt for the agent is crafted to encourage:
  - Using domain knowledge and engineering intuition.
  - Forming and updating hypotheses.
  - Maintaining a living task list.
  - Following document references and alternative explanations.
  - Delivering clear, actionable answers grounded in evidence.

---

#### [01:26:40 ~ 02:25:06] Agent Design Considerations and System Prompt

- Additional real-world scenarios illustrate the need for:
  - Associating documents with **specific projects** to focus the search scope.
  - Utilizing **metadata such as authorship, timestamps, and document relevance** to prioritize retrieval.
  - Handling **very long documents** by chunking and context-aware retrieval.
  - Searching for **adjacent or related information** via section headers and metadata.
- Agent reasoning must:
  - Adapt its **search strategy** (exhaustive vs. hypothesis-driven) based on query nature and user persona.
  - Maintain **notes and task lists** that evolve with new findings.
  - Decide when enough information is gathered to provide a useful answer.
- The speaker notes challenges with **memory efficiency** and processing speed on local machines, emphasizing that GPU-based processing will be necessary for scale.
- The agent system prompt is extensively developed, including:
  - Framing the agent as a **knowledgeable aerospace engineering expert and consultant** with access to a vast document archive.
  - Encouraging the agent to use **domain expertise in physics, failure modes, regulatory context, and operational realities**.
  - Guiding the agent to:
    - Understand the user’s explicit question and underlying problems.
    - Form hypotheses and plan investigations.
    - Search with intent, using domain synonyms and contextual understanding.
    - Engage deeply with documents, not just extract keywords.
    - Follow leads and references across documents.
    - Update task lists dynamically and reprioritize.
    - Know when to stop searching (enough evidence gathered).
    - Provide synthesized, coherent answers with source citations.
    - Communicate clearly, like a senior colleague, not a search tool.
    - Respect time constraints and be transparent about uncertainty.
- The prompt discourages hardcoding specific examples, instead aiming for **flexibility and domain intuition-driven reasoning**.
- Plans are made for **integrating NASA’s aerospace thesaurus and acronyms** to improve query expansion and retrieval.
- The agent is to be designed as a **reasoning engine using search as a tool**, not just a search engine.

---

#### [02:56:18 ~ 03:05:00] Domain Terminology and Vocabulary Management

- The aerospace domain is **highly standardized** with extensive controlled vocabularies, including thousands of acronyms and technical terms.
- NASA provides a publicly available **thesaurus with over 18,000 standardized terms**, including relationships like synonyms, broader/narrower terms.
- The system will integrate these vocabularies to:
  - Expand user queries intelligently.
  - Improve retrieval relevance by mapping acronyms to full terms (e.g., "ISP" to "Specific Impulse").
- Since fine-tuning large models is not planned, a **retrieval-augmented approach** using a small re-ranking model (e.g., 6 billion parameters) will help quickly identify relevant domain terms in queries.
- This approach is scalable and can be updated as vocabulary evolves.
- The speaker references existing open-source repositories and Python scripts for loading NASA terminology.
- The vocabulary management is a critical piece to **bridge user input and document content effectively**.

---

#### [03:10:19 ~ 04:30:43] Agent Skeleton Implementation and Tooling

- The speaker discusses implementing an initial **agent skeleton** using Claude with streaming and tool-calling support.
- The agent will have capabilities to:
  - Search documents.
  - Retrieve document chunks.
  - Maintain internal notes and task lists dynamically.
- The system prompt and tools are designed to be **minimally opinionated**, allowing the agent to decide what to note and what tasks to create or update.
- Notes serve as a workspace for internal reasoning and important information.
- Task lists are living documents capturing what to investigate, what is done, and what remains.
- The agent will present all notes and tasks transparently in the terminal for easy debugging.
- Emphasis is placed on **iterative development**, refining the system prompt and tooling based on observed agent behavior.
- The speaker acknowledges challenges with memory management and processing on the Mac and plans to offload heavy processing to GPU-enabled VMs.
- The agent is intended to **think and reason like a senior aerospace engineer**, synthesizing information rather than simply retrieving it.
- The project management approach is flexible and pragmatic, emphasizing **understanding the user and domain deeply before coding**.
- The agent’s system prompt and task management approach are designed to encourage:
  - Planning investigations.
  - Hypothesis testing.
  - Following leads.
  - Delivering clear, contextual responses.

---

#### [04:46:55 ~ End] Wrap Up and Next Steps

- Notes on improving the agent’s note management:
  - Instead of replacing old notes, the agent should **append and build on previous notes** like a human would.
- The speaker plans to continue refining the **agent's to-do list and notes** functionality.
- The next stream or sessions will focus on:
  - Enhancing the **agent’s reasoning and task planning**.
  - Improving **tool integration and streaming output**.
  - Processing the full document corpus on GPU infrastructure.
- Emphasis remains on developing a **robust, domain-aware, reasoning-driven agent** that can **reduce search time from hours to minutes** in highly technical aerospace engineering contexts.
- The speaker encourages **running multiple simulations** to discover edge cases and improve the agent’s design iteratively.

---

### Key Insights

- Building a RAG system for aerospace documents requires **careful document processing and metadata extraction**, especially for complex documents with formulas, tables, and images.
- The core challenge is **not just retrieval**, but building an **agentic system that reasons like a human expert**, synthesizes information, and follows leads intelligently.
- Understanding **user personas and their search behaviors** is crucial for designing the agent’s reasoning style and interaction model.
- The aerospace domain’s **highly standardized vocabulary** and specialized jargon must be integrated via a **domain vocabulary and thesaurus** to enable effective query expansion and matching.
- The agent system prompt must be **flexible and encourage domain intuition**, avoiding hardcoded templates but guiding reasoning and search strategies.
- The system needs to handle **large-scale document corpora** efficiently, requiring scalable infrastructure and smart chunking/context management.
- Iterative development with **simulations of agent-user interactions** is invaluable to discover unknowns and refine the agent’s behavior.
- The agent should maintain **dynamic task lists and notes** for tracking investigation progress, enabling transparent and explainable responses.
- The final system aims to be a **trusted, time-saving assistant** that mitigates risk and preserves critical knowledge in aerospace engineering.

---

### Keywords

- Retrieval-Augmented Generation (RAG)
- Aerospace documents
- Document processing
- Formula extraction
- Table extraction
- Image understanding
- Domain-specific language
- NASA thesaurus
- Semantic search
- Intelligent agent
- Domain intuition
- Task list and notes
- Query expansion
- Knowledge management
- On-premise deployment
- Open-source LLMs
- Claude AI
- Embeddings and re-ranker
- Metadata search
- Simulation-based design
- Agent system prompt

---

### FAQ

**Q: What is the scale of documents supported by the system?**  
A: The system is designed to support at least **85,000 documents**, currently tested on 10,000, with scalability to 100,000+ documents.

**Q: How does the system handle complex document formats?**  
A: It uses advanced open-source models for **extracting formulas, tables, images, and chunking** to convert documents into searchable, semantically rich data.

**Q: What makes this system different from traditional keyword search?**  
A: Rather than keyword matching, it uses a **reasoning agent** that understands domain context, expands queries intelligently, follows cross-document references, and synthesizes answers.

**Q: How is domain knowledge integrated?**  
A: Through the use of **NASA’s aerospace thesaurus and acronym dictionaries**, combined with domain-specific embeddings and re-ranking models to map queries to technical terminology.

**Q: Who are the target users?**  
A: Senior engineers with deep domain knowledge and junior engineers learning the domain, each requiring different search and reasoning styles supported by the agent.

**Q: What is the role of the agent’s task list and notes?**  
A: They serve as a **dynamic workspace** for internal reasoning, tracking hypotheses, outstanding questions, and investigation progress, enabling iterative and transparent search processes.

**Q: Is the system cloud-based?**  
A: The document processing and storage are planned to be **on-premise**, but the reasoning agent currently uses **cloud-based LLMs** like Claude for advanced reasoning.

---

This extensive summary captures the depth and breadth of the project discussed in the video transcript, organized according to the original content flow, and emphasizing technical details, user understanding, agent design, and system implementation considerations.

# [Building Agents That Think Like Engineers at scale | Sub-Agents & Tools | 10K+ NASA Docs | Part 5](https://www.youtube.com/live/nmsKOr-wdFU?si=slCxTYKARJw5i-Kg)
### Summary of the Video Transcript: Building a Scalable RAG System for Aerospace Documents

---

#### [00:00:07 ~ 00:02:53] Introduction and Project Overview

- The speaker introduces the ongoing project of building a Retrieval-Augmented Generation (RAG) system designed to work at scale for a fictional company named Meridian Aerospace.
- The project scope involves handling a large corpus of approximately 85,000 to 100,000 aerospace-related documents spanning from the 1950s to the present (circa 2025), covering roughly 75 years of technical content.
- The initial focus is on processing a subset of 10,000 documents, with plans to scale infrastructure to manage all 85,000+ documents reliably.
- These documents include complex technical materials such as scanned copies, PDFs, technical diagrams, formulas, graphs, and tables.
- The RAG pipeline leverages open-source models for embedding, re-ranking, and visual-language modeling (VLM), achieving 90–95% accuracy in extracting text, formulas, and images from documents dating back to 1954.
- The previous streams (4–6 sessions, many lasting 5–10 hours) involved deep dives into building and validating document processing pipelines, including hierarchical chunking and content extraction.
- The data source is NASA’s Technical Report Server (NTRS), which provides well-scanned, unclassified aerospace documents with rich metadata.
- The speaker mentions plans to release GitHub code to allow users to download and process tens of thousands of documents themselves.

---

#### [00:03:22 ~ 00:09:47] Document Processing Capabilities and Agent Development

- The system handles complex tables and technical diagrams, including documents with intricate layouts and many pages.
- The RAG pipeline can analyze images, generate accurate descriptions, and extract content across different document types, including liquid engine propulsion systems and turbo pump technical documents.
- The document processing system also extracts vector embeddings using advanced models (e.g., quantized 4-billion parameter embeddings, running locally).
- The re-ranker model currently used is a 0.6 billion parameter model due to hardware constraints but is planned to be upgraded when deploying on GPUs.
- The search pipeline is fully open-source and capable of deployment on secure IT infrastructure, critical for handling sensitive or classified aerospace data.
- The speaker discusses developing an intelligent agent that orchestrates document search, reasoning, and tool usage for effectively answering user queries.
- The agent’s initial skeleton is capable of calling tools, managing notes and tasks dynamically, and iterating over search results to narrow down answers.
- There is active work on improving how the agent updates notes and task lists to avoid information overload and maintain concise, relevant summaries.
- The agent is designed to simulate real user behavior (e.g., a senior officer named Sandra) to better understand how domain experts interact with the system and refine the agent’s reasoning.
- The speaker stresses the importance of planning and simulating user interactions over rushing into coding, highlighting that domain intuition and user goal understanding are key to building effective AI tools.

---

#### [00:10:38 ~ 00:25:46] Challenges with Notes, Tasks, and System Prompt Design

- The agent struggles with replacing notes entirely and not consistently updating tasks, causing potential confusion or loss of important context.
- The speaker discusses refining prompt engineering to encourage the agent to produce concise bullet-point style notes rather than verbose essays.
- The agent is instructed to update tasks only after completing a specific task (which may involve multiple searches) rather than after every search action.
- There is discussion around rate limits with APIs (e.g., Anthropic and OpenAI tokens per minute) and the need to increase credits for smoother testing.
- Enhancements to the agent’s workflow and prompt structure are underway to improve accuracy and coherence in multi-turn reasoning.
- The agent’s tools are modularized into categories such as search documents, get document chunks, get adjacent context, and visual tools.
- The speaker emphasizes the importance of filters (e.g., by date range, document type, chunk type) to increase precision in search results.
- There is a plan to create a comprehensive documentation detailing all tools, their rationales, key parameters, and usage patterns for future reference and development.
- The agent toolset is designed to support reasoning processes rather than just document retrieval, enabling engineers to investigate failures, trace references, and synthesize custom reports.
- Visual tools for images, complex tables, and formulas are introduced as last-resort options when text-based tools fail or when verification is necessary.
- The approach prioritizes accuracy over API cost or processing time, reflecting the critical nature of aerospace document analysis.

---

#### [00:27:12 ~ 00:43:20] Tool Design Philosophy and Document Metadata Handling

- Tools are conceptualized as simple JSON objects but are powerful building blocks that enable the agent to solve complex, domain-specific problems creatively.
- The speaker outlines various specialized tools:
  - Search documents with filters (e.g., timeline-based search).
  - Retrieve document chunks, including adjacent chunks for context expansion.
  - Search within a specific document or section.
  - Retrieve entire pages or document sections based on headings.
  - Visual context tool to capture bounding boxes from PDFs for verification of formulas or diagrams.
  - Parallel search tool to perform broad, multi-query searches simultaneously to quickly map relevant information.
  - Spawn research threads as sub-agents to perform deep dives on specific investigation tasks.
- There is recognition of missing metadata in some chunks (e.g., section headings, abstract, report dates), which are critical for effective filtering and retrieval.
- The system plans to extract and normalize report dates from standardized report pages or fallback to using the first two pages’ images processed by VLM if metadata is missing.
- Formula extraction is complex because formulas alone lack semantic meaning; they require contextual descriptions to be searchable and interpretable.
- The speaker references the mathematician Srinivasa Ramanujan to highlight the conceptual depth of formulas and the necessity of attaching meaning or notes for effective retrieval.
- Complex tables are processed mostly via descriptions and semantic search over those descriptions.
- Visual verification tools are important for confirming formulas or diagrams, especially when OCR or chunking may miss inline math or graphical elements.
- The system is designed to favor text-based tools initially, resorting to visual tools only when necessary due to higher computational costs and complexity.

---

#### [00:43:21 ~ 01:01:47] System Prompt and Agent Behavior Design

- The system prompt for the agent embeds domain intuition, turning the model into a knowledgeable aerospace engineer with years of experience.
- Agents are encouraged to use tools creatively and efficiently rather than applying tools blindly.
- The system prompt is part of a living document that evolves with development, simulations, and real-world feedback.
- Randomness in the agent’s behavior is controlled to ensure creativity without compromising domain knowledge.
- The agent is designed to avoid underworking or overworking for problems by balancing effort according to task complexity.
- Visual tools are treated as expensive fallbacks, and the agent is guided to prioritize text-based reasoning.
- The agent’s working memory is segmented into notes, tasks, and tools, each updated via specific tool calls to maintain clarity and avoid information overload.
- The speaker stresses the importance of carefully drafting the system prompt and tool descriptions to influence agent behavior without restricting creativity.
- The approach treats the agent as a single “brain” combining domain understanding, tool use, and prompt engineering, rather than splitting responsibilities among multiple teams.
- The document processing pipeline and metadata schema are constantly refined to improve coverage of headings, abstracts, symbols, formulas, bounding boxes, and report dates.
- Extensive validation is performed on sample documents to verify extraction quality, bounding box accuracy, and metadata completeness.

---

#### [01:39:22 ~ 02:04:06] Toolset Deep Dive and Metadata Structure

- The speaker goes into a detailed review of the planned tools and their parameters, including:
  - Search documents with filters on timeline, formula types, chunk types.
  - Get adjacent chunks to expand context around a center chunk.
  - Get document chunks for reading entire documents or sections.
  - Get full page or section based on metadata like section headers.
  - Visual tools for complex tables, figures, and formula verification.
  - Parallel search tool to run multiple queries simultaneously for broad coverage.
  - Spawn research threads (sub-agents) for parallel deep investigations.
- Discussion on how metadata like section headers, bounding boxes, and notes are stored and used.
- The importance of storing bounding boxes for all chunks to enable visual verification tools.
- Metadata for formulas includes descriptions from surrounding text to enable semantic search.
- Visual tools can capture screenshots of PDF regions for verification when chunked text is incomplete or missing.
- Parallel search tool acts as a broad exploratory hit, useful for mapping information quickly and deciding targeted follow-ups.
- Sub-agents receive context and a clear task goal, enabling them to conduct focused research and return summarized findings.
- The tools are designed to support reasoning workflows with strong filters rather than just raw search.

---

#### [02:04:07 ~ 03:01:19] Development Plan and System Improvements

- The speaker outlines development tasks:
  - Adding missing metadata like abstracts, headings, formulas, bounding boxes.
  - Improving date extraction and normalization with fallback to VLM processing of PDF pages.
  - Enhancing formula extraction to include surrounding context for better semantic retrieval.
  - Implementing bounding box calculations for formulas by interpolating between text bounding boxes.
- The system is tested on sample PDFs with mixed results; some formula extraction fails and needs debugging.
- The speaker emphasizes the importance of accuracy and completeness in metadata to ensure effective agent reasoning.
- Changes to document chunking and heading extraction are discussed to improve section retrieval accuracy.
- The agent tool specification document is updated to reflect new tools and their parameters.
- The system prioritizes year-based date filtering over precise date filtering due to variability in document date formats.
- Plans to remove old, deprecated search tools and start fresh with clearly defined agent tool specifications.
- The agent architecture is described as a single brain integrating context, tools, and domain knowledge, designed for accuracy and creativity.
- Logging, debugging, and validation tools are emphasized for tracking tool calls, search results, and agent reasoning.

---

#### [03:01:20 ~ 07:02:17] Agent Tool Implementation, Testing, and Iteration

- The speaker tests search documents tool extensively, validating that it can search within documents, filter by document ID, and return relevant chunks with metadata.
- The agent is able to reason over complex queries involving formulas, tables, and technical jargon.
- The system differentiates between search documents and get document chunks tools, with clear roles for each.
- Adjacent chunks tool allows context expansion by retrieving paragraphs before and after a given chunk.
- Conversation history is maintained to support follow-up questions and context continuity.
- The speaker discusses disabling re-ranker temporarily to reduce computational load during testing.
- The agent is tested with multiple models (e.g., Haiku, Sonnet, Claude) to compare performance and hallucination rates.
- The speaker encourages incremental tool integration and validation rather than large batch coding.
- The agent is capable of updating notes and tasks dynamically during a session.
- The system supports parallel search queries to explore multiple hypotheses simultaneously.
- The agent tool specification documentation is kept up to date with progress and is the single source of truth for tool design.
- Visual tools for viewing images, figures, and diagrams are implemented, with support for bounding box extraction from PDFs.
- Image post-processing and noise reduction are noted as future improvements.
- The agent spawns research threads (sub-agents) for complex investigations, passing relevant context and task goals.
- The speaker discusses best practices for sub-agent launches to avoid recursion and maintain efficiency.
- The agent is tested on very complex queries requiring cross-document reasoning, image analysis, and deep synthesis.
- Logging and debugging of agent behavior and tool calls are emphasized to ensure reliability.
- The agent is designed to balance creativity and accuracy, avoiding over-reliance on any single tool.
- The interaction mode supports large context windows (up to millions of tokens) to handle extensive aerospace documentation.

---

#### [07:02:18 ~ 11:00:00+] Final Notes and Reflections

- The speaker shares personal background and consulting experience building similar RAG systems for regulated industries (pharmaceutical, defense, finance).
- The importance of starting with smaller, simpler document sets before scaling to large corpora is stressed.
- The system is designed to operate on-premises with open-source models to meet security and compliance needs.
- The agent is tuned to handle complex aerospace engineering queries involving formulas, tables, and visual data.
- The speaker encourages viewers to engage with the project, try the released code, and learn from the development process.
- The architecture separates concerns cleanly between document processing, embedding, re-ranking, agent reasoning, and tool orchestration.
- The system continuously evolves through user feedback, simulations, and technical improvements.
- Future work includes improving formula bounding boxes, refining heading extraction, enhancing date filtering, and expanding visual tool capabilities.
- The speaker emphasizes that designing an effective agent is a long-term process requiring deep domain understanding and thoughtful tool integration.
- The video concludes with plans to continue development after breaks, focusing next on agent UI and deployment.

---

### Key Insights

- Building a scalable RAG system for aerospace documents requires deep integration of document processing, embedding, reasoning agent, and specialized tools.
- Metadata completeness and accuracy (headings, abstracts, formulas, bounding boxes, dates) is critical for effective retrieval and reasoning.
- Agent design must simulate real user behavior and domain intuition; planning and simulation are more important than immediate coding.
- Tools must be modular, simple, and powerful building blocks; the agent should creatively orchestrate tool usage rather than blindly calling them.
- Visual tools are important but expensive fallbacks; text-based semantic search and filtering are primary.
- Parallel search and sub-agent spawning enable efficient large-scale research and reasoning.
- System prompts and tool descriptions shape the agent’s domain expertise and reasoning style.
- Continuous validation, logging, and iteration are essential to maintain accuracy and improve system performance.
- The entire system is designed to run on-premises with open-source models for security, compliance, and cost reasons.

---

### Keywords

- RAG (Retrieval-Augmented Generation)
- Aerospace document processing
- Semantic search
- Vector embeddings
- Document chunking
- Formula extraction
- Visual-language models (VLM)
- Agent orchestration
- Metadata filtering
- Parallel search
- Sub-agent spawning
- Tool design
- Domain intuition
- Open-source models
- On-premises deployment
- Document metadata (headings, abstracts, dates, bounding boxes)

---

### FAQ

**Q: What is the scale of the document corpus targeted?**  
A: Approximately 85,000 to 100,000 aerospace technical documents spanning 75 years from the 1950s to 2025.

**Q: What types of documents are processed?**  
A: Scanned PDFs containing text, technical diagrams, formulas, tables, and graphs.

**Q: What models are used for embeddings and re-ranking?**  
A: Quantized 4-billion parameter embedding models run locally; re-ranker is a 0.6 billion parameter model, with plans to upgrade on GPUs.

**Q: How is formula search handled given formulas lack semantic meaning?**  
A: Formulas are indexed alongside surrounding descriptive notes to enable semantic search and contextual retrieval.

**Q: What is the role of the agent?**  
A: The agent manages tool orchestration, reasoning, note/task management, and simulates domain expert behavior to answer complex queries.

**Q: How are visual elements like images and complex tables handled?**  
A: Textual descriptions are indexed for semantic search; visual tools capture bounding boxes and screenshots for verification when necessary.

**Q: How is time-based filtering implemented?**  
A: Document years are extracted and normalized, with filtering usually on the year level rather than exact dates or months.

**Q: What is the strategy for tool design?**  
A: Tools are simple, modular JSON objects providing specific filtered search or context retrieval capabilities; the agent uses these creatively.

**Q: Can the system operate fully on-premises?**  
A: Yes, leveraging open-source models and local GPU infrastructure to meet security and compliance requirements.

**Q: How are sub-agents used?**  
A: Sub-agents are spawned as specialized research threads for deep investigations, receiving context and task goals from the main agent.

---

This comprehensive summary captures the core content of the video transcript, organized by the original flow and covering technical depth, challenges, design rationales, and development plans.

# [Agentic Tools & UI Implementation | Building AI Agents for 10K+ NASA docs from 1960s-2025s | Part 6](https://www.youtube.com/live/Ji8lhhDYXKA?si=QpTsTc-zeGgerFJI)
### Summary of the Video Transcript (Segmented by Timestamp)

---

#### - [00:00:18 ~ 00:01:30] Introduction and Overview of the Project

Raj introduces the live stream session, marking day six of building a production Retrieval-Augmented Generation (RAG) system for NASA documents. This system is intended to manage and process a large corpus of 85,000 NASA-related documents. The session is conducted on Twitter Live instead of YouTube, indicating a trial of a new platform. The main goal is to review the progress made so far and clarify what the project entails, providing newcomers with an initial understanding of the system being built.

---

#### - [00:01:12 ~ 00:03:44] Project Concept: Meridian Aerospace Document System

The project revolves around a fictional midsize aerospace company, Meridian Aerospace, which contracts with NASA and other space agencies. The company manages an archive of 85,000 documents ranging from the 1950s to the present. Raj shows examples of these documents, highlighting their complexity: they contain OCR-extracted text, formulas, graphs, tables, diagrams, and images.

The system under development processes 10,000 documents initially, aiming to scale to the full 85,000. Raj emphasizes the difficulty in handling complex tables and formulas, explaining that prior live streams covered the development of a robust document processing pipeline capable of extracting and indexing this heterogeneous content effectively.

---

#### - [00:03:47 ~ 00:06:05] Document Processing Pipeline and Open Source Models

The document processing pipeline is a core component, capable of extracting tables, formulas, images, and diagrams. The system chunks documents, extracts context, and creates a searchable index with metadata filters such as date.

Importantly, all processing is done using open-source models, which makes the system viable for sensitive or classified data scenarios where cloud solutions like AWS are not permissible. This ensures the deployment can be on-premises for security compliance, especially relevant for aerospace and defense documents.

The agent architecture includes a capability to spawn multiple sub-agents for parallel or sequential tasks, enhancing scalability and modularity. Raj reflects on the importance of deeply understanding the user's domain and problem space to design an agent that truly mimics the cognitive patterns of aerospace engineers, rather than just assembling a technical system.

---

#### - [00:06:24 ~ 00:09:37] Dataset Sampling and Document Diversity

Raj details the approach to building a representative sample of documents from different decades (1950s through 2000s) and types (tables, images, formulas). This diversified subset is crucial for stress-testing the system against worst-case scenarios like poor OCR quality on old documents or complex table structures.

The system achieves approximately 90% accuracy on formula extraction using open-source models. The documents are noisy and diverse, including blacked-out classified sections, symbols, nomenclature, and mixed media content, all of which complicate extraction and indexing.

---

#### - [00:09:38 ~ 00:11:31] Project Value and Real-World Context

Raj explains that while this is a fictional project, a real-world implementation of such a system would carry a substantial budget—easily $250k to $300k—with ongoing maintenance costs. The project has significant value given the complexity and scale of aerospace technical documentation.

He encourages beginners to explore the project and learn from the existing code base and live streams, underscoring the educational value of the system for those interested in document AI.

---

#### - [00:11:32 ~ 00:17:46] Agent Testing and Tool Integration

Raj transitions to demonstrating the agent built in previous sessions. The agent uses a query related to aerospace engineering—specifically, a trade-off analysis for afterburner configurations. The agent processes document chunks, performs parallel searches, and invokes multiple tools (e.g., adjacent chunks, document info) to find relevant information.

The agent demonstrates sophisticated behavior: it performs hit-and-get queries, filters using metadata, and processes images and formulas contextually. It employs domain intuition rather than rule-based prompts, leveraging models pre-trained on aerospace engineering language and thought patterns.

The agent also uses sub-agents to delegate research tasks, running parallel or sequential passes through documents, and has a task and notes system to track progress and context.

---

#### - [00:17:47 ~ 00:22:42] Agent Design Philosophy and Sub-Agent Architecture

Raj elaborates on the cognitive model behind the agent: the system is designed to think like an aerospace engineer, understanding the realities and nuances of the document corpus. This includes managing document age, OCR quality, and verifying uncertain data visually (via screenshots) when the text extraction is potentially inaccurate.

Sub-agents are clones of the main agent but limited to prevent recursive spawning, ensuring controlled exploration of threads. Sub-agents receive tasks and context from the parent, perform focused searches, and maintain their own notes.

Iterations are controlled to balance depth of search with response time. Raj plans to increase the iteration cap to allow deeper exploration.

---

#### - [00:22:43 ~ 00:28:53] Agent Evaluation and Accuracy Testing

The system's response quality is evaluated, showing high accuracy (graded A+). Raj notes that forcing the agent to use sub-agents exclusively may reduce performance slightly but serves as a useful test.

He discusses the need for a UI to visualize agent behavior and document sources, emphasizing the importance of seeing images, tables, and formulas as the agent processes them.

---

#### - [00:29:00 ~ 00:37:25] Handling Formula Bounding Boxes and Visual Region Capture

Raj discusses a key challenge: formulas do not currently have bounding box information in the document processing pipeline, unlike other elements. To address this, the system uses heuristic bounding boxes based on the vertical and horizontal layout of text and formulas, leveraging inline math detection and page layout information.

He describes how adjacent boxes (above and below a formula) help estimate the formula’s bounding box, allowing visual region capture for quality verification.

This method accommodates edge cases like formulas at the start or end of a page and accounts for inline math that OCR engines typically fail to parse accurately.

---

#### - [00:37:26 ~ 00:43:29] Code Caution and Change Management

Raj stresses the importance of careful code changes, especially given the complexity and interdependencies in the pipeline. He advises thorough code reviews and communication before modifying critical parts to avoid pipeline failures that can waste hours of debugging.

He also discusses nuances in bounding box indexing and encourages understanding the codebase fully before implementing changes.

---

#### - [00:46:23 ~ 00:51:56] Creating Complex Test Cases and Agent Behavior Fine-Tuning

Raj requests the creation of complex use cases involving formulas, equations, and tables that simulate real user queries without explicitly naming specific equation numbers or document references. This tests the agent’s ability to proactively locate and verify relevant information.

He reviews agent responses, confirming the system can identify and verify formulas, including LaTeX-rendered math and Greek symbols, demonstrating the system's capability to handle highly technical mathematical content.

---

#### - [00:52:00 ~ 00:56:56] Finalizing Tools and Visual Region Capture Use

Raj confirms the visual region capture tool’s critical role in verifying inline math and complex formulas, which can sometimes be partially missed in text extraction. The tool captures screenshots of formula regions for manual or automated verification.

He emphasizes the need to complete tool specifications precisely, as even minor misunderstandings in tool behavior can degrade overall system accuracy.

---

#### - [00:56:57 ~ 01:08:42] Preparing for UI Development and Code Management

Raj shifts focus to building a test UI that can display agent responses, sources, images, and bounding boxes to facilitate iterative testing and debugging.

He discusses pushing the current code to GitHub, including .gitignore management for public docs and research code, ensuring the repository remains manageable and secure.

---

#### - [01:09:58 ~ 01:32:51] Agent Interaction and Tool Usage Analysis

Raj runs the agent with visual region tools enabled and observes the agent’s reasoning steps, tool calls, and use of visual verification. He probes the agent’s rationale for when and why it chooses certain tools, encouraging reflection and honesty in the agent's decision-making simulation.

He finds the visual region tool useful for confirming complex math rendering and ensuring alignment with source PDFs, especially for older documents with poor OCR.

He discusses system prompt design—opting for minimal explicit instructions about tool usage to maintain natural agent reasoning rather than over-guided behavior.

---

#### - [01:33:00 ~ 01:49:19] Managing Document Scale and Embedding Efficiency Challenges

Raj talks about the scale challenges of handling 10,000 documents, which may contain up to 500 million tokens. He explains the computational cost of embedding such a large token space, noting that searching across all tokens for each query is impractical.

He discusses the need for filtering by timeline or project context to reduce the search space—e.g., limiting queries to recent documents or specific subsets.

He explains that embedding dimension size (1024 dimensions preferred over 2048 for efficiency) and memory requirements (several GBs of RAM per query) are critical considerations for deployment.

Parallel query handling and GPU acceleration are planned to improve scalability.

---

#### - [01:50:00 ~ 02:10:27] UI Development Planning and Streaming API Design

Raj plans to develop a simple front-end UI using XJS for querying the agent, displaying responses, images, and sources. The UI will initially be minimal, focusing on functionality rather than aesthetics.

He discusses API design considerations, including whether to stream responses in real-time or batch them, favoring streaming for better interactivity.

Plans include integrating the UI with the backend agent API, enabling real-time visualization of agent reasoning and tool calls.

---

#### - [02:33:17 ~ 02:44:25] Codebase Familiarization and Stream Stability Issues

Raj advises thorough codebase reading to understand all relevant files, emphasizing the importance of grasping the full document processing and agent pipeline.

He notes technical streaming issues during the live broadcast (frame drops) due to bandwidth or software constraints, which do not impact the development process.

---

#### - [02:50:44 ~ 03:20:44] UI Testing, Latency Issues, and Feature Enhancements

Raj runs the API and UI, noting some lag related to the re-ranker model, which he temporarily disables to improve responsiveness.

He observes memory usage patterns, suspecting full precision loading of models and plans to optimize this.

He highlights UI behavior where agent text and tool calls render in a concatenated flow, proposing improvements like LaTeX rendering support for mathematical formulas.

He confirms the agent can fallback to image-based verification when symbol extraction fails.

He demonstrates inspecting tables, formulas, and images in the UI, noting some UI rough edges but overall functional.

---

#### - [03:27:56 ~ 04:10:59] Sub-Agent UI and Interaction Improvements

Raj tests sub-agent spawning in the UI. He wants the sub-agent interface to be more user-friendly, with real-time updates, auto-scrolling within the task box, and clear separation of tool calls and text outputs.

He discusses UI theming, consistent flow, and minimalistic design for tool call displays.

Raj requests the front-end skill be used for UI refinement.

---

#### - [04:12:15 ~ 04:18:54] Table Rendering and Document Metadata

Raj tests displaying tables extracted from documents. He notices some tables render as descriptions rather than structured markdown tables and plans to improve this.

He confirms the system can extract tables accurately, but the UI needs to better represent them.

---

#### - [04:19:40 ~ 04:26:34] Roadmap and Future Work: Scaling, Domain Knowledge, and RAG Improvements

Raj outlines the upcoming focus: processing the full 10,000 document batch on GPU-enabled VM infrastructure, ensuring failure rates remain below 2-3%.

He emphasizes the importance of domain-specific acronyms and taxonomy management (using NASA's 18,000 keyword dataset, focusing on 2,000-3,000 relevant terms) to enhance retrieval quality.

He discusses the strategy for reducing search space and complexity by applying filters like timeline, recent projects, and document relevance.

He explains how sub-agents will help parallelize and distribute complex queries, allowing the system to handle vast document corpora efficiently.

Raj expects initial failure rates of 30-40% during development but expects this to improve with iteration and context management improvements.

---

### Key Insights and Core Concepts

- **Complex Document Processing Pipeline:** The project handles heterogeneous aerospace documents with intricate tables, formulas, and images using open-source models for OCR, formula extraction, and table parsing.

- **Open-Source and On-Premises Deployment:** Critical for handling sensitive classified information, avoiding cloud dependency, and providing flexibility in model choice.

- **Agent Architecture with Sub-Agents:** The system uses a primary agent with the ability to spawn sub-agents to distribute tasks, increasing efficiency and search depth.

- **Domain Intuition in Agent Design:** The agent mimics aerospace engineers’ reasoning patterns, using domain knowledge to prioritize tools and verify data visually.

- **Formula Bounding Boxes and Visual Region Capture:** Complex heuristics estimate bounding boxes for formulas to enable accurate visual verification and quality assurance.

- **Scale and Efficiency Challenges:** Handling 10,000+ documents with hundreds of millions of tokens requires filtering strategies, embedding dimension trade-offs, GPU acceleration, and efficient indexing mechanisms.

- **UI Development for Real-Time Interaction:** The UI aims to present agent responses, tool calls, images, tables, and formula renderings in an interactive, user-friendly manner.

- **Iterative Development and Failure Management:** Targeted failure rates below 3%, with plans to reprocess failures and improve accuracy via fallback tools and domain-specific metadata.

- **Taxonomy and Acronym Integration:** Use of NASA’s domain-specific keywords to improve retrieval relevance and agent understanding.

---

### Keywords

- Retrieval-Augmented Generation (RAG)
- Document Processing Pipeline
- Optical Character Recognition (OCR)
- Formula Extraction
- Table Parsing
- Open-Source Models
- On-Premises Deployment
- Sub-Agent Architecture
- Domain Intuition
- Visual Region Capture
- Bounding Boxes
- Embedding Space
- Quadrant Vector Search
- GPU Acceleration
- Real-Time UI
- Aerospace Engineering Documents
- Domain-Specific Acronyms and Taxonomy
- Failure Rate Management
- Parallel Processing
- Metadata Filtering

---

### FAQ

**Q1: Why use open-source models instead of cloud services?**  
A1: Open-source models allow deployment on-premises, essential for handling sensitive or classified aerospace documents that cannot be uploaded to cloud services due to compliance and security restrictions.

**Q2: How does the system handle complex formulas and tables?**  
A2: The system uses specialized OCR and layout detection models, estimates bounding boxes for formulas, and extracts inline math. It captures visual regions for quality assurance and integrates these into the searchable index.

**Q3: What is the role of sub-agents?**  
A3: Sub-agents are lightweight clones of the main agent that handle specific subtasks or research threads, enabling parallel exploration of complex queries without recursive spawning, improving scalability and efficiency.

**Q4: How does the system manage the massive scale of documents?**  
A4: By filtering queries with metadata (e.g., date ranges), using project-based scoping, and employing embedding space optimizations to reduce search load. GPU acceleration and parallel processing further support scale.

**Q5: What UI features are prioritized?**  
A5: A simple, interactive interface to enter queries, display agent responses, view sources, images, tables, and formula renderings, and monitor sub-agent activities in real-time with auto-scrolling and tool call visualization.

**Q6: How is accuracy maintained given noisy OCR and document variability?**  
A6: The system uses fallback mechanisms like visual region capture, thorough domain modeling, and iterative testing with diversified datasets. It aims for failure rates below 3% and incorporates manual and automated verification steps.

---

This detailed summary captures the entire scope, technical depth, and development plan of the NASA document RAG system as described in the transcript, adhering to the original structure and providing an in-depth understanding for readers or practitioners interested in such complex document AI systems.

# [Processing 10K Documents on a H100 (Qwen) | GPU Infrastructure, Scaling Math, VLLM & Ollama | Part 7](https://www.youtube.com/live/Wd-DZNKE87Y?si=qnQkqhGKLGDgD2cv)
### Summary of Video Content: Building a Production RAG System for NASA Documents (Day 7)

---

#### [00:00:14 ~ 00:06:48] Introduction and Overview of Project Scope and Document Complexity

The session begins with an introduction to the seventh day of building a production retrieval-augmented generation (RAG) system designed for processing and querying a massive archive of NASA documents—approximately 85,000 in total. The streaming session aims to advance the document processing pipeline, specifically scaling to handle 10,000 documents in this phase.

The fictional client, Meridian Aerospace, is a consulting firm specializing in rocket technology, certification, and technical analysis. Their document corpus is highly heterogeneous, spanning scanned copies, handwritten notes, faxed documents, re-scanned and photocopied papers from as early as the 1950s through the 2000s. These documents also contain heavy domain-specific acronyms and jargon such as $LOX$ (liquid oxygen), $ISP$ (specific impulse), and many others, which pose challenges for generic agents.

The goal is to deliver a fully open-source, on-premises deployable system that complies with strict IT and government security requirements, running efficiently on GPU-equipped infrastructure. This system must accurately handle complex document types, including heavy use of mathematical formulas (expressed in LaTeX), tables, images, and diagrams.

Visual examples from the 1954 and 1963 NASA PDFs demonstrate the complexity: some documents are clean and well-structured with simple tables, whereas others feature multi-page spanning tables, complex figures, and heavily degraded images (e.g., crack magnification photos that resemble abstract paintings). The system must extract all this content into structured markdown preserving semantic information for downstream tasks.

The presenter highlights the exhaustive research and development conducted over previous streams (30-40 hours), including downloading over 10,000 documents overnight from NASA's NTRS API. Samples from different decades and document types were carefully selected to ensure diversity and robustness in the processing pipeline. The approach focuses on solving for representative samples to generalize to the entire corpus.

---

#### [00:06:48 ~ 00:14:45] Agent Development and Querying Workflow

The team built an intelligent agent to interact with the documents. Early development involved deep domain research—understanding aerospace engineers’ terminology, workflow, problem solving styles, and typical queries. This domain knowledge was essential to design effective prompts and tool usage that spike the model’s intuition akin to a senior aerospace engineer.

The agent supports chunk-level querying with access to metadata, sources, and document hierarchy (sections and subsections). It can perform multi-threaded or parallel research by spawning sub-agents, each responsible for specific tasks, allowing efficient parallelization of document research without recursive loops.

In an example query—validating performance coding against reported methodologies—the agent filters through hundreds of document chunks (e.g., 400 relevant chunks among thousands), simulating a "needle in a haystack" search. The system includes:

- **Document Info Chunking**: Identifying relevant paragraphs and sections.
- **Visual Reasoning**: Verifying formulas and images by screenshotting PDF regions.
- **Hierarchy Access**: Utilizing document tree structures to pinpoint exact sections.

The agent outputs answers with extensive LaTeX-rendered mathematical formulas and references to up to 41 source documents, which can be inspected by the user. The UI displays agent notes and tasks, allowing traceability of reasoning and work flow.

A key UX feature is the presentation of visual figures alongside textual answers. Users can click on images to verify original diagrams or tables, crucial because some visual data cannot be easily inferred from text alone. The source control system is designed to let users skim PDFs directly within the interface, navigating via arrows and seeing highlighted sections related to the query, avoiding the clunky experience of opening separate PDFs or losing context.

Transparency and trust-building are emphasized: since the agent might miss small details (estimated 5% error margin), users treat it as a research assistant or supercharger rather than a definitive oracle. The system’s source visibility encourages verification, reducing blind reliance on the model.

---

#### [00:14:45 ~ 00:42:41] Document Processing Pipeline Design and GPU Infrastructure Planning

The main focus shifts to scaling document processing to 10,000 documents using a VLM (Vision Language Model) on a single NVIDIA H100 GPU (80-96GB VRAM) in Azure. The model used is a $32$ billion parameter "Quinn 32B V-instruct" version, balancing accuracy and resource constraints.

The pipeline flow for each document includes:

- **Document Loading**: Reading PDFs with complex layouts.
- **Sequential Subprocesses**: Identifying figures, tables, formulas sequentially.
- **Parallel Image Processing**: Running multiple images detected in a document concurrently through the VLM to extract captions and descriptions.
- **Chunking**: Splitting documents into semantically meaningful chunks (~250 tokens minimum), preserving paragraph boundaries without overlap.
- **Output JSON**: Final structured representation includes bounding boxes (BB boxes) for layout, markdown tables, LaTeX formulas, and image descriptions.

The pipeline uses IBM’s open-source *Dockling* for layout detection and paragraph extraction. The embedding model (Pin 4B) generates vector representations for retrieval. A quadrant system manages embeddings and document retrieval.

Resource planning carefully models concurrency limits based on GPU VRAM, CPU cores, RAM, and token context sizes. Key constraints and assumptions include:

- GPUs: Single H100 with 80-96GB VRAM (actual measured 96GB).
- CPU Cores: 48-96 cores.
- RAM: Approx. 256GB system RAM.
- Max context length: 10,000 tokens per request.
- Parallelization: Targeting 15-20 documents processed simultaneously, each spawning 4 VM workers (tasks).
- Each document has internal parallelism for image extraction.
- Dockling models consume ~2GB RAM.
- GPU concurrency limit: 32 requests maximum; balanced by VM workers per doc and documents in parallel.

Through detailed token and memory calculations, the presenter determines the "sweet spot" for parallel processing: 15 documents with 4 VM workers each (60 total concurrent requests) to maximize throughput without exceeding memory or compute limits, yielding an estimated processing time of approximately 6.5 hours for 10,000 documents.

The presenter discusses dynamic token allocation with VLM for further optimization but concludes gains (~2 hours saved) are not worth the complexity given the already maxed-out system utilization.

A critical discovery is the actual VRAM available on the H100 is 96GB (not 80GB as initially assumed), which allows increased concurrency—possibly up to 30 documents in parallel with 3 workers each—further boosting throughput.

The choice of numeric precision for model weights is debated: FP16, FP8, INT8, Q8_0 quantization formats are considered. The team opts to prioritize accuracy over speed, preferring FP16 or Q8 quantized models with minimal accuracy loss. The deployment will use VLM for inference with fallback options to Olama (another open-source serving solution) if package or driver issues arise.

---

#### [00:42:41 ~ 01:39:00] Cloud Infrastructure Setup and Disk Management

The presenter details the practical challenges of cloud VM management:

- Initial separation of two VMs: one with NASA documents (no GPU), another with GPU (no documents).
- Solution: Detach the 1TB disk containing downloaded NASA documents from the data VM and attach it to the GPU VM.
- Created snapshots for data safety to avoid re-downloading the massive dataset.
- Verified H100 GPU memory availability (~96GB VRAM).
- Checked system specs: 96 CPU cores, 256GB RAM, ample disk space.
- The new setup unlocks higher throughput and more workers for document processing.

The presenter reflects on his limited cloud expertise (more familiar with AWS and GCP than Azure), but manages to configure and mount the disks successfully. He confirms the ability to run the entire pipeline on a single GPU VM with direct access to all documents.

---

#### [01:39:00 ~ 02:13:58] Deployment Planning and Codebase Setup

Attention turns to deployment strategy and codebase readiness:

- The pipeline and models need to be packaged for deployment on the GPU VM.
- Docker is used to containerize Quadrant (for embeddings and retrieval).
- Python environment setup includes installing latest packages, managing dependencies, and creating working directories.
- The deployment plan includes a **quick start guide**, minimal dependencies, and monitoring/logging capabilities to observe pipeline progress in real-time.
- The code should accept a directory input pointing to the 10,000 documents and automatically process them end-to-end.
- The first milestone: process a single document fully to verify pipeline stability.
- Subsequent steps: scale to 10 or 100 documents, then full batch processing.
- Monitoring tools should provide updates on chunking, embeddings, source extraction, and errors.
- Emphasis on modular design: embedding models, quadrant, document processing pipelines should be separable and composable.

The presenter stresses that the system must be robust and production-ready, not just quick experimental scripts. The final system will expose the quadrant index as an API to integrate with the agent.

---

#### [02:13:58 ~ 03:30:02] Technical Challenges and Debugging

The session covers ongoing technical challenges:

- Errors encountered when running GPU jobs, particularly with VLM packages and dependency mismatches.
- Discussion about installing VLM from GitHub directly instead of pip to avoid CUDA version conflicts.
- Version mismatches between CUDA 12 and CUDA 11.05 cause runtime errors.
- Consideration of using a stable, slightly older VLM package or switching back to Olama if issues persist.
- The presenter highlights the complexity of maintaining GPU inference environments due to dependency and driver issues.
- Use of Docker containers is favored to encapsulate the environment and reduce runtime errors.
- Encouragement to install and test models without screens (terminal multiplexers) for easier log access and debugging.
- The presenter plans to pause and resume the stream for gym breaks, continuing later to solve the issues.

---

#### [03:30:02 ~ 04:02:53] Advice on Software Engineering and Career Insights

The presenter addresses live chat questions and provides career advice:

- Emphasizes that building such complex systems requires a solid foundation in computer science and software engineering.
- Cloud Code and low-code tools can build simpler applications but not complex, large-scale systems like this.
- Encourages learning fundamentals and progressively increasing project complexity.
- Shares personal experience: a solo developer building a multi-month, multi-person project in a few weeks with 10x quality.
- Explains the choice of IBM Dockling over alternatives like Overlapping Layout detection for document layout analysis.
- Highlights the scale: processing about 10,000 documents averaging 50 pages each, totaling half a million to 750,000 pages.
- The project involves detailed extraction of formulas, tables, images, and text for accurate vector embedding and retrieval.

---

#### [04:02:53 ~ 04:48:00] Final Wrap-Up and Next Steps

The session concludes with:

- Final attempts to resolve package and GPU driver issues.
- Plans to test deployment with a single document, then incrementally scale.
- Acknowledgment of the difficulty of debugging runtime errors related to VLM and GPU packages.
- The fallback plan is to use Olama models if VLM proves too unstable.
- Commitment to completing the project by the end of the week.
- Encouragement for viewers to check out previous live streams for context.
- Invitation to connect on LinkedIn for further discussions.

---

### Key Insights and Core Concepts

- **Complex Document Processing**: Handling heterogeneous, noisy, and domain-specific documents requires sophisticated document layout detection, formula parsing, and image extraction.
- **Domain-Adapted Agents**: Effective retrieval-augmented generation systems benefit from domain-specific understanding and user workflow modeling.
- **Scalable Pipeline Design**: Balancing sequential and parallel processing steps with GPU resource constraints is critical for throughput.
- **Memory and Token Management**: Detailed calculations of VRAM, CPU cores, RAM, and token limits guide concurrency and batching strategies.
- **Deployment Engineering**: Containerization, dependency management, and remote VM configuration are as important as model accuracy.
- **Transparency and UX**: Showing sources, images, and document hierarchy alongside answers builds user trust and facilitates verification.
- **Fallback Strategies**: Having alternative inference engines (Olama vs. VLM) mitigates risk from deployment issues.
- **Career Advice**: Complex AI systems require solid software engineering skills combined with domain knowledge and iterative development.

---

### Keywords

- RAG System
- NASA Documents
- Document Processing Pipeline
- Vision Language Model (VLM)
- Quadrant Embeddings
- GPU (NVIDIA H100)
- Document Chunking
- Formula Extraction (LaTeX)
- Document Layout Detection (Dockling)
- Parallel Processing
- Memory and Token Management
- Docker Containerization
- Open Source Models
- Deployment and Monitoring
- Domain-Specific Agent
- Source Transparency
- FP16, FP8, INT8 Quantization
- Cloud VM Management
- Error Debugging and Dependency Management
- Software Engineering Fundamentals

---

### FAQ

**Q: Why is the project focusing on 10,000 documents now, when the dataset has 85,000?**  
A: Processing 10,000 documents is the current scaling step to validate pipeline performance and resource management before tackling the full set.

**Q: How does the system handle noisy and degraded documents?**  
A: By combining layout detection, parallel processing, and manual sampling of diverse document types, the system extracts structured markdown including formulas, tables, and image descriptions.

**Q: What models and precision are used?**  
A: The primary model is a 32B parameter QuAn V-instruct variant, deployed in FP16 or Q8 quantization for a balance of accuracy and efficiency.

**Q: How is concurrency managed on a single GPU?**  
A: Through detailed resource calculations, balancing documents processed in parallel and VM workers per document, capped by GPU VRAM and CPU cores.

**Q: What happens if VLM package has runtime issues?**  
A: The team will fallback to Olama models and containers, prioritizing stable deployments over cutting-edge performance.

**Q: How are sources presented to users?**  
A: Via an integrated viewer showing PDFs with highlighted sections, alongside extracted images and LaTeX-rendered formulas for full transparency.

---

This comprehensive summary encapsulates the detailed technical walkthrough, project management considerations, and practical deployment challenges encountered during day seven of this ambitious large-scale document processing project.


# [Processing 10K Documents on a H100 (Qwen 32B) | VLLM Optimization, OCR, Docling, Scaling | Part 8](https://www.youtube.com/live/aDUXnOfblcA?si=i3yQnR2mJAFhxlCs)
### Summary of Video Content on Building a Production-Scale RAG System for Complex Rocket Science Documents

---

#### [00:00:12 ~ 00:03:24] Introduction and Project Context  
The presenter introduces this session as a continuation of an extensive series focused on building a production-ready Retrieval-Augmented Generation (RAG) system for a massive repository of rocket science documents. This project deals with over 85,000 documents spanning a wide time range—from the 1950s scanned copies to handwritten notes from the 1960s and current documents. These documents are highly complex, containing technical jargon, domain-specific acronyms, mathematical equations, formulas, graphs, and technical diagrams.

The goal is to build a scalable, production-grade system capable of ingesting and processing this large corpus. Although currently working with a smaller subset of approximately 10,000 documents, the system architecture is designed to scale beyond 100,000 documents, providing robust handling at scale.

The project is framed around a fictional company called Meridian Aerospace, operating in a consulting engineering space sector, partnering with NASA. This provides a realistic and challenging use case for document ingestion and processing, given the technical complexity and volume of documents involved.

Key challenges highlighted include:
- Handling documents with various formats: scanned copies, handwritten notes, and digital documents.
- Extracting metadata, symbols, and technical jargon from documents rich with domain-specific language.

---

#### [00:03:20 ~ 00:05:58] Document Vocabulary and Model Strategy  
The project leverages NASA’s domain-specific vocabulary corpus, specifically selecting 3,000 to 4,000 rocket science-related terminologies from an 18,000-strong vocabulary set covering biological, earth, and physical sciences, among others. Importantly, the team opts not to fine-tune any models but rather uses open-source pre-trained models.

The pipeline is split into two primary components:
1. **Document Processing**: Entirely based on open-source models, specifically using the Quen model for embeddings and document understanding.
2. **Agent Layer**: Utilizes cloud-based models for downstream querying and interaction, which can be swapped out for any other model depending on the deployment environment.

The session plans to continue from previous work, focusing on ingestion, processing, and exposing APIs for the 10,000 documents.

---

#### [00:05:18 ~ 00:08:35] Hardware and Deployment Challenges  
The presenter discusses significant technical difficulties encountered, particularly with CUDA environment issues affecting Visual Language Models (VLMs). The system relies on an Azure-hosted Nvidia H100 GPU with 96GB of VRAM, which is essential to handle concurrent processing of large batches of documents.

Resource planning includes:
- Processing 24 documents per batch.
- Each document parallelized across three sub-workers handling tables, images, formulas, and figures.
- A total of 72 concurrent VLM workers.
- Embedding batch size of 120.

Memory allocation:
- 33GB for model weights.
- Approximately 58GB reserved for concurrency and KV cache.
- Around 5GB for embeddings.

The processing time per document is estimated to be around 67 seconds, though this can vary.

Due to stability and compatibility challenges with the VLM deployment, the team decides to fall back to Olama's Q8 quantized model, which offers 95–97% accuracy, nearly matching the original model but with easier deployment and fewer issues.

---

#### [00:08:40 ~ 00:12:34] Data Acquisition and Initial Setup  
The team successfully acquired a dataset of 10,414 documents from NASA’s Technical Report Server (NTRS), including documents dating back to 1954. The download process took approximately 7 hours due to API rate limits.

The presenter emphasizes the importance of efficient ingestion and processing, aiming to complete the embedding and metadata extraction for all 10,000+ documents within approximately 8 hours, which is considered a good performance for such a complex workload.

Cleanup and environment setup commands are run remotely via VS Code on the Azure VM. The rented H100 GPU setup is costly (~$700/day), but the presenter secured a monthly package for $5,000, allowing for sustained experimentation.

---

#### [00:14:15 ~ 00:28:56] Model Deployment and Precision Optimization  
The team experiments with model precision and quantization to optimize performance and memory usage. They explore:
- Using the VLM with FP8 floating-point precision, which the H100 GPU is optimized for.
- Trade-offs between Q4 and Q8 quantization levels for speed and accuracy.
- Dynamic precision allocation, e.g., FP16 for vision components and Q8 for language components.
- Managing GPU memory fragmentation and concurrency to avoid crashes and maximize utilization.

The presenter notes the complexity of deploying models in production, including handling dependencies, version mismatches, and wrapping models with appropriate APIs.

They also discuss the advantage of dynamic context allocation with VLMs versus static allocation in embeddings, which can lead to better resource utilization, especially with varying document sizes and concurrent user loads.

---

#### [00:29:29 ~ 01:31:53] Service Management, API Exposure, and Verification  
The team sets up and verifies various services, including:
- The Olama inference server.
- Embedding models.
- The VLM server deployed via Docker.

They expose necessary ports for local and remote access and run pre-flight verification checks to ensure all components are running correctly.

Scripts for starting, stopping, and monitoring services are refined to support seamless restarts and operational stability, which is crucial for long-running batch processes.

---

#### [01:41:02 ~ 01:51:38] Detailed Document Processing Architecture  
A detailed visual and conceptual overview of the document processing pipeline is presented:

- **Document Loading**: 10,414 documents are loaded, each handled by a dedicated thread in a thread pool (24 documents processed concurrently).
- **Chunking and Extraction**: Each document is broken down into logical chunks (~1000 tokens each), preserving document order for retrieval coherence.
- **Element Extraction Pipelines**: Parallel pipelines extract tables, formulas (converted to LaTeX), images (with descriptions), and textual blocks.
- **Parallel VLM Workers**: Each document has up to three VLM workers operating concurrently on different extraction tasks.
- **Embedding Generation**: Embeddings are generated from chunks using quantized 8-bit models for efficiency.
- **Vector Database**: The embeddings are stored in a vector database (Cauldron), supporting semantic search.

The architecture emphasizes concurrency balanced against hardware limits, with 72 concurrent VLM requests maximized across the GPU memory budget.

---

#### [01:53:17 ~ 02:06:15] Real-World Document Examples and Metadata Extraction  
Sample documents ranging from 1954 to the 1960s demonstrate the complexity of the data, including heavy noise, scanned pages, extensive tables, and diagrams.

The system performs extensive metadata extraction such as bounding boxes, noise removal, symbol detection, and formula recognition, all critical for accurate semantic search and retrieval.

The processing pipeline is designed to handle worst-case documents, ensuring robustness across a wide range of document qualities.

---

#### [02:13:22 ~ 02:27:16] Runtime Monitoring, Memory Allocation, and Performance Tuning  
The team monitors GPU memory utilization and compute load during test runs, noting high memory usage (~90% of 96GB VRAM).

Key insights include:
- The trade-off between static memory reservation and dynamic allocation (around 80-90% VRAM usage for safety).
- The importance of queuing and retry mechanisms for robustness.
- The challenge of handling spikes in concurrent requests or document complexity.
- The necessity of monitoring tools to track processing phases and document statuses in real-time.
- The goal of minimizing downtime and avoiding full pipeline restarts after failures by checkpointing processed documents and resuming from failures.

---

#### [02:40:31 ~ 03:10:21] Processing Speed and Bottlenecks  
Initial tests show that processing three documents takes approximately 10 minutes, implying naive extrapolation to the full corpus would require over 20 days, which is impractical.

Analysis reveals bottlenecks, particularly in the OCR step and the symbol extraction phase, with dockling OCR running on CPU being significantly slower than desired.

Switching OCR processing to GPU reduces processing time roughly by half, improving throughput but still requiring optimization.

The presenter acknowledges the variability in document complexity (e.g., documents with 100+ pages or numerous tables increase processing time significantly).

---

#### [03:22:20 ~ 04:12:40] OCR Strategy and Processing Pipeline Optimization  
The team debates the use of OCR for all documents, noting that many NASA documents already have selectable text, making OCR redundant and expensive.

They consider strategies to prefer native text extraction, falling back to OCR only when necessary (e.g., scanned documents without extractable text).

Dockling’s bitmap analysis and coverage thresholds determine when full-page OCR is triggered, but the current threshold leads to excessive and inefficient OCR runs on images and scanned content.

Disabling OCR outright or setting a higher bitmap threshold yields significant speed improvements (~half the previous processing time), enabling more parallel workers.

The trade-off is some documents may lose text extraction fidelity if OCR is disabled.

---

#### [04:28:54 ~ 05:42:57] Worker Parallelism, Memory Usage, and Cloud Costs  
After disabling OCR, the system runs more efficiently, processing documents faster and freeing GPU memory for additional workers.

The presenter discusses the economics of cloud GPU rentals, noting the high cost of running H100 GPUs (~$700/day), but also credits allowing monthly access at a reduced price (~$5,000/month).

They emphasize the importance of optimizing batch sizes, worker counts, and memory allocation to maximize throughput within budget constraints.

---

#### [05:46:28 ~ 07:00:44] Model Quantization and Memory Utilization Issues  
The team experiments with different model sizes and quantization schemes:

- Using a 7B or 8B parameter model with quantization to reduce VRAM usage.
- Encountering unexpectedly high VRAM consumption (~90+ GB) even with small models.
- Investigating possible reasons, such as full precision loading instead of FP8 or 8-bit quantized loading.
- Considering batch requests to reduce redundant VLM calls for tables and formulas.

They highlight the need to balance accuracy with performance, noting that smaller models may fail to generate correct JSON outputs or accurately parse tables, which is critical for domain-specific document processing.

---

#### [07:04:12 ~ 08:18:30] Document Size Variability and Pipeline Design Considerations  
The presenter discusses variability in document length (some PDFs are over 70 pages, others over 200+), which impacts batch processing time and resource allocation.

They note the necessity of granular progress tracking per document, including counts of tables, formulas, and chunks, to identify slow documents and optimize throughput.

They acknowledge that some documents require significantly more processing time due to complexity, and parallelization must accommodate this variability.

The discussion extends to pipeline inefficiencies, such as VLM calls being made redundantly for each table or formula, suggesting batching or caching could improve performance.

---

#### [08:33:59 ~ 08:51:52] Confirmation of OCR Disabling and Resulting Performance Gains  
Disabling OCR in favor of relying solely on VLM-based layout and extraction models leads to significant runtime improvements and memory savings.

The presenter admits that enabling OCR was a mistake given the nature of the NASA documents, which are mostly clean and text-selectable PDFs.

With OCR disabled, documents process in under a minute in some cases, enabling increased concurrency and worker parallelism.

Formula extraction accuracy is confirmed, with LaTeX extraction and image descriptions working properly.

---

#### [09:00:52 ~ 10:13:31] Final Model Testing, Memory Usage, and Worker Scaling  
Testing continues with the 7B and 8B parameter models, investigating memory consumption and concurrency limits.

The team notes that even with 7B models, VRAM usage is unexpectedly high, limiting the number of parallel workers to about 5-6 before crashing.

They experiment with token lengths (8k, 16k, 32k) and memory allocation percentages (70-90%) to find a stable and efficient configuration.

It’s determined that around 70% VRAM allocation is prudent to avoid crashes, allowing for a balance between throughput and stability.

---

#### [10:18:52 ~ 11:47:36] Monitoring, Progress Tracking, and Architecture Planning  
The presenter stresses the importance of robust monitoring and checkpointing systems to track:
- Number of documents processed.
- Number of documents remaining.
- Which processing phase each document is in (e.g., OCR, embedding, formula extraction).

They want to build an architecture that supports:
- Resuming processing from failure points without redoing completed work.
- Automated notifications for failures or progress milestones.
- Efficient queuing and load balancing for worker pools.

Finally, the presenter requests an architectural design document outlining the entire system, broken down into phases with clear milestones, validation steps, and production readiness criteria.

---

### Key Insights and Takeaways

- **Complexity of Processing Heterogeneous Documents:** Handling rocket science documents spanning decades with mixed media (scans, handwritten notes, digital) requires a robust, multi-modal extraction pipeline.
- **Hardware Considerations:** High-end GPUs like Nvidia H100s are critical for scaling, given the large number of concurrent workers and model sizes.
- **Precision and Quantization Trade-offs:** Using FP8 and quantized 8-bit models balances accuracy and memory consumption, crucial for deploying large models on limited hardware.
- **OCR Optimization:** Avoiding unnecessary OCR on documents with selectable text greatly improves throughput and reduces GPU memory pressure.
- **Parallelization Strategy:** Efficient concurrency involves a thread pool for documents combined with sub-workers per document handling different extraction pipelines.
- **Progress Tracking and Fault Tolerance:** Essential for long-running batch jobs to allow resuming without data loss or duplication.
- **Cost Implications:** GPU rental costs are substantial, emphasizing the need for careful resource management and optimization.
- **Pipeline Architecture:** A modular, open-source-based pipeline combining document parsing, element extraction, embedding generation, and vector storage supports scalable semantic search.
- **Practical Deployment Challenges:** Version mismatches, package dependencies, and model API compatibility require significant engineering effort beyond model training and inference.

---

### High-Level Architecture Overview (Visualized Conceptual Summary)

1. **Input Layer:**  
   - 10,000+ PDFs loaded concurrently with thread pool.

2. **Preprocessing:**  
   - Dockling or similar layout detection for text blocks.
   - Bitmap thresholding to decide OCR necessity (disabled or fallback only).
   - Noise removal, bounding box annotation.

3. **Element Extraction (Parallel within each document):**  
   - Tables → markdown/text extraction.
   - Formulas → LaTeX conversion.
   - Images → description generation.
   - Symbols and technical metadata extraction.

4. **Embedding Generation:**  
   - Quantized 8-bit language models (Quen, Olama) produce semantic embeddings.
   - Batch size tuned for GPU VRAM.

5. **Vector Storage:**  
   - Embeddings stored in Cauldron or similar vector DB for retrieval.

6. **API Layer:**  
   - Serve queries via cloud or on-prem agents.
   - Load balancing and concurrency management.

7. **Monitoring and Management:**  
   - Real-time progress dashboard.
   - Checkpointing and failure recovery.
   - Email/log notifications for SLA adherence.

---

### FAQ

**Q:** Why disable OCR despite scanned documents?  
**A:** Most NASA documents have selectable text; OCR is expensive and redundant. OCR is enabled only as a fallback for truly scanned-only pages.

**Q:** What is the role of quantization in models used?  
**A:** Quantization reduces model weight size and VRAM usage, enabling deployment of large language models on limited GPU memory with minimal accuracy loss.

**Q:** How is concurrency managed?  
**A:** 24 documents processed in parallel, each with up to 3 parallel sub-tasks (tables, formulas, images), totaling 72 concurrent VLM workers.

**Q:** What bottlenecks remain?  
**A:** Dockling OCR and symbol extraction are slowest steps; GPU acceleration and disabling unnecessary OCR improve speed. Model loading and memory management also pose challenges.

**Q:** How is fault tolerance achieved?  
**A:** The system tracks which documents are processed and checkpoints progress to resume after failures without reprocessing.

---

### Final Remarks  
This video details a complex, real-world production pipeline for processing a massive corpus of technical aerospace documents, blending deep learning models, GPU hardware optimization, and engineering best practices to build a scalable RAG system. The journey reveals the intricacies of balancing accuracy, speed, cost, and robustness, offering valuable insights for anyone building large-scale document ingestion and semantic search systems in specialized domains.


# [H100 Pipeline Rewrite: 28 Days to 2.5 for 10K docs, vLLM FP8 Optimization, OCR | NASA RAG | Part 9](https://www.youtube.com/live/gNxiIsRXwRc?si=32W-gmA9Ssdu3nGz)


# [Parallel Processing 10K Documents on a H100 | Multi-Instance Load Balancing, Celery & Redis |Part 10](https://www.youtube.com/live/a9pNRWj5670?si=BF-mC6eY9UpP7snW)
### Summary of Video Content with Timestamps and Detailed Analysis

---

#### Introduction and Overview of the Project  
- [00:00:07 ~ 00:03:38]  
The video begins with the host introducing the session as a continuation of a previous livestream (Day 9 Part 1). The purpose of this stream is to document progress on a complex project involving large-scale document processing, specifically technical diagrams embedded in documents. The goal is to scale a system that currently processes about 10,000 documents efficiently.

Each document is typically rich in content such as tables, formulas, and diagrams. The system uses models such as the 20-32 billion parameter versions of Visual Language Models (VLMs) for document understanding, with accuracy rates between 90-95%. Dockling, an open-source document processing framework, is used primarily for layout detection and bounding box extraction but not OCR. The current hardware setup involves a single NVIDIA H100 GPU with 96GB VRAM, loaded with a 7 billion parameter model variant for inference.

The key challenge addressed in this section is the efficiency of processing 10,000 documents. A naive approach would take several days to weeks to process, so the team is focused on optimizing the infrastructure for parallel batch processing and true GPU-level parallelism. The previous 12-hour debugging stream revealed that the initial approach was on the wrong track, leading to a complete redesign of the infrastructure to better mimic how ML inference platforms operate at scale.

---

#### Core Technical Challenge: Dockling and PDF Processing Bottleneck  
- [00:07:22 ~ 00:12:59]  
A major bottleneck arises from Dockling’s dependency on a PDF processing package (referred to as `pypdfm` or `pdfm2`), which severely limits threading and multiprocessing capabilities. Although Dockling supports multiprocessing, this particular PDF package locks the thread during processing, effectively serializing PDF conversion tasks.

This results in a paradoxical situation: despite running multiple GPU-based Dockling workers in parallel, the PDF processing step forces serialization, leading to no speed gains from parallelism during this step. For example, converting a 70-page document takes approximately 50 seconds; ideally, processing three documents in parallel would still take about 50 seconds, but due to the threading lock, processing three documents sequentially still takes 150 seconds.

To work around this, the team is leveraging the large GPU VRAM by running multiple Dockling service instances (workers) in parallel, each assigned to its own port. Each instance consumes about 6-7 GB of VRAM, meaning with 50 GB available (after accounting for the 34 GB used by the VLM model), around 7 Dockling workers can be run simultaneously. This approach allows parallelization at the service level rather than within a single process, mitigating the threading lock issue.

Furthermore, the system first processes documents through Dockling once, then offloads the processed output to CPU memory, avoiding repeated calls to Dockling and reducing GPU VRAM pressure. The VLM model is then invoked separately for further processing using the freed-up VRAM, supporting efficient batch and parallel processing.

---

#### Project Management and Documentation Strategy  
- [00:12:59 ~ 00:16:09]  
The host emphasizes the importance of structured project documentation. The project is divided into phases (Phase 1 through Phase 6), and each phase is documented meticulously with details such as architecture diagrams, rationales for design decisions, encountered issues, and future plans.

The documentation acts as a timeline and context repository, allowing anyone who picks up the project to quickly understand the decisions made previously, the current state, and next steps. This approach saves extensive debugging time and helps maintain clarity despite the complexity and frequent changes in infrastructure and services.

For relatively small or medium-sized projects, this phase-based documentation approach is recommended as a best practice. It enables systematic progress tracking and context retention, which is crucial when working solo or in small teams without formal project management resources.

---

#### Experimental Setup: Parallel Dockling Workers and Performance Metrics  
- [00:15:58 ~ 00:22:33]  
The team sets up three Dockling instances running in parallel on different ports with a simple round-robin load balancing scheme. The goal is to validate whether true parallelism can be achieved despite the PDF processing package’s threading limitations.

Initial results show that processing three documents (each about 70 pages and dense with diagrams and formulas) in parallel takes about 66 seconds total, compared to 50 seconds for a single document processed sequentially. This speedup corresponds to nearly 3x faster throughput, confirming that the parallel multi-instance approach is effective.

The host calculates the implications for processing 10,000 documents: at approximately 3 minutes per document and 7 parallel workers, it would still take about 3 days to complete the entire batch. Although this is a significant improvement from the original worst-case estimate of 29 days, it highlights that document processing at this scale requires careful balancing of parallelism and GPU resource allocation to avoid congestion.

---

#### Handling Real-World Issues and Improvisation  
- [00:36:59 ~ 00:40:21]  
The host reflects on the challenges faced due to the limitations in the Dockling and PDF processing stack. The workaround—running multiple Dockling instances in parallel—is an improvisation rather than a perfect solution. Such adaptations are common in real-world projects where ideal libraries or frameworks do not exist or have limitations.

The host advises viewers that rigid plans rarely survive contact with reality in complex projects. Flexibility, incremental improvements, and continuous learning (including leveraging AI assistants like Claude) are crucial to progress. While some teams might conduct formal proof-of-concepts (PoCs) before committing to solutions, the host opts for a more direct, iterative approach to maintain momentum.

The results of the parallelization effort are promising: processing speed improved by nearly 3x, the GPU memory usage was well-managed, and phase one of the project was successfully completed.

---

#### Transitioning to Phase Two and Project Scaling  
- [00:46:45 ~ 00:55:13]  
The team prepares to transition into phase two of the project. Before proceeding, they plan to update the production architecture and phase one documentation to reflect all recent progress and changes.

They discuss the importance of understanding the foundation laid in phase one as it serves as the base for future phases. There is a focus on validating parallelism and ensuring that no hidden serialization or bottlenecks remain before scaling further.

The host mentions potential performance anomalies, such as why processing three documents in parallel took 66 seconds instead of closer to 50 seconds. This leads to further investigation and refinement.

---

#### Project Insights and Recommendations for Designing Pipelines  
- [01:30:49 ~ 01:38:27]  
In a Q&A style discussion, the host shares insights on how to approach designing document processing pipelines, especially at enterprise scales:

- Understand the problem and scale before designing the pipeline. There is no one-size-fits-all solution.
- For enterprise-scale projects processing tens of thousands of documents, infrastructure efficiency becomes a critical challenge.
- Focus on the types of documents (legal, financial, charity, etc.) to understand content complexity (tables, stamps, formulas).
- Use open-source tools like Dockling for layout detection and embedding generation frameworks like Quadrant.
- Design system prompts and agent logic carefully when exposing chatbots or AI assistants to users, including escalation paths to humans when AI confidence is low.
- Security considerations are important but can be managed by controlling what data is embedded and exposed.
- Emphasizes the importance of embedding textual information and using VLMs for multimodal understanding.

The host also highly praises the AI assistant Claude for helping solve complex coding and architectural challenges, noting that it accelerates learning and development significantly compared to other coding assistants like Copilot or Codex.

---

#### Pipeline Testing and Monitoring  
- [01:42:53 ~ 01:52:54]  
The host demonstrates running the Dockling workers and the VLM model concurrently, monitoring GPU utilization and processing speeds. The system shows expected fluctuations in resource consumption as documents with mixed content (images, formulas, text) are processed.

Initialization of Dockling instances takes about 40-50 seconds but is a one-time cost amortized over long runs. The host notes that the system is stable enough to run continuously for days, processing thousands of documents efficiently.

---

#### Final Notes and Next Steps  
- [03:40:24 ~ 03:41:37]  
The session concludes with a recap that document processing is working well with caching and monitoring in place. The next immediate goal (phase four) involves optimizing batching for the VLM models, which should reduce processing time further.

The host apologizes for a brief audio issue but expresses confidence in the current progress and readiness for the next deployment phase. The project is positioned well for incremental improvements, with clear milestones and documentation guiding the team forward.

---

### Key Insights and Core Concepts

- **Infrastructure Bottlenecks:** The biggest bottleneck in scaling document processing was the PDF processing package’s threading lock, which serialized an otherwise parallelizable workload.
  
- **GPU VRAM Management:** Efficient utilization of GPU memory by running multiple Dockling instances (each consuming ~7GB VRAM) in parallel enabled overcoming the threading bottleneck at the service level.

- **Batch Processing & Parallelism:** True parallelism was achieved by balancing the number of Dockling workers and VLM instances, with trade-offs between throughput and GPU congestion.

- **Phase-Based Documentation:** Maintaining detailed, phase-specific documentation is vital for clarity, debugging, and knowledge transfer in complex projects.

- **Iterative Development & Improvisation:** Real-world projects require flexibility; ideal frameworks rarely exist, so pragmatic workarounds and incremental improvements are key.

- **AI-Assisted Development:** Advanced AI tools like Claude can significantly accelerate problem-solving, learning, and debugging in complex system design.

- **Security & Data Handling:** When exposing AI systems to end-users, design for data privacy, confidence thresholds, and escalation paths to human operators.

- **Scalability Considerations:** Processing 10,000+ documents with complex multimodal content demands carefully architected pipelines that balance compute resources, memory, and latency.

---

### Suggested Keywords

- Document Processing Pipeline  
- Dockling Framework  
- PDF Processing Bottleneck  
- GPU Parallelism  
- Visual Language Models (VLM)  
- Batch Processing  
- Large-Scale Document Understanding  
- Infrastructure Optimization  
- Phase-Based Project Documentation  
- AI-Assisted Code Development  
- System Design for Scalability  
- Multi-Instance Load Balancing  
- Enterprise Document Processing  
- Thread Locking in PDF Libraries  
- GPU VRAM Management  

---

### FAQ

**Q: What is the main bottleneck in processing large batches of documents using Dockling?**  
A: The main bottleneck is the PDF processing package used by Dockling, which serializes document processing due to thread locking issues, preventing true parallelism within a single process.

**Q: How does the team overcome the threading limitation in Dockling?**  
A: By running multiple Dockling service instances in parallel on different GPU memory slices and ports, effectively achieving parallelism at the service level rather than within a single process.

**Q: Why is phase-based documentation important in this project?**  
A: It helps maintain clear context, tracks architectural decisions, and simplifies debugging and scaling by documenting the evolution of the system step-by-step.

**Q: What hardware is used for processing?**  
A: A single NVIDIA H100 GPU with 96GB VRAM is used, with memory split between the VLM model (~34GB) and multiple Dockling instances (~7GB each).

**Q: How long does it take to process 10,000 documents?**  
A: With current optimizations and 7 parallel workers, it can take roughly 3 days, a significant improvement over the original estimate of nearly a month.

**Q: How is AI used in the development process?**  
A: AI assistants like Claude help with debugging, code generation, and conceptual understanding, significantly reducing development time and complexity.

---

This detailed summary captures the technical depth, system design considerations, challenges, and solutions described in the video transcript, following the original structure and timestamps for clarity and completeness.


# [Building Production RAG for 10K+ NASA Docs (Scales to 85K+): Rocket Schematics and more! (Part 11)](https://www.youtube.com/live/ZewbP6tNJwI?si=ymKAOxOmGNf26ba0)


# [H100 Optimization & Parallel Processing at 180 Pages/Min | Scaling to 10K NASA Documents | Part 12](https://www.youtube.com/live/0G2ESVa9hR8?si=XWSQYepjpw5KWhAE)
### Summary of Video Transcript: Building a Scalable Document Processing System for 10,000+ NASA Documents

---

#### [00:00:04 ~ 00:01:04] Introduction to the Project and System Overview  
The presenter introduces the live stream focused on building a production-ready backend system designed to process over 10,000 NASA documents, scalable to even 85,000-100,000 documents. The system is designed to handle complex document types that include formulas, tables, diagrams, and technical images. It is built entirely using open-source models running on a single NVIDIA H100 GPU with 95GB of VRAM. The infrastructure is containerized using Docker and implements a hybrid CPU-GPU processing pipeline.

---

#### [00:00:33 ~ 00:02:21] Document Complexity and Pipeline Development  
NASA documents are highly complex, featuring dense indexing, numerous formulas, tables, graphs, and high-resolution images, making standard PDF chunking approaches inadequate. Over several previous streams, the team completed the entire document processing pipeline, focusing on robust layout analysis and formula recognition. The latest challenge is scaling this pipeline efficiently to process 10,000 documents. The approach involves parallel processing with batching on a single H100 GPU, and the pipeline architecture was rewritten to separate GPU and CPU services to improve efficiency and reuse components. The presenter hints at writing a blog post to share detailed insights from these extensive live coding sessions.

---

#### [00:02:30 ~ 00:04:08] Achieving Parallel Processing and Throughput Goals  
Initially, the system struggled to process even a single document efficiently. Now, it can process 24 documents in parallel, each with its own Dockling instance for layout detection, fully utilizing the GPU through batching. The current throughput is approximately 80 to 100 pages per minute, with a target throughput of about 150 pages per minute to meet the processing deadlines for tens of thousands of documents. The documents vary significantly in size and complexity, with some PDFs being very large in file size (e.g., 170 MB) but containing fewer pages, often due to high-resolution scans.

---

#### [00:03:35 ~ 00:05:57] Handling Large PDFs with Dynamic Downscaling  
High-resolution scanned documents, despite having fewer pages, pose a challenge due to their large file size and processing load. The team tested dynamic downscaling of images within PDFs to reduce file size and processing overhead, but initial tests showed no significant time improvement. The presenter describes working offline due to health issues but emphasizes continuing development and testing. The system runs on a Python virtual environment, with celery workers managing concurrency. Restarting and flushing services are common steps to ensure system stability during testing.

---

#### [00:06:56 ~ 00:13:09] Scaling Logic and Performance Issues  
The team implements logic to downscale any PDFs larger than 50 MB dynamically, reducing their resolution to balance quality and processing time. However, downscaling risks losing important details, which could affect downstream tasks like OCR and image recognition. The presenter experiments with setting thresholds for scaling factors based on file size ranges (e.g., 0.5 scale for >100 MB, 1.0 for 50-75 MB, etc.). Problems with Dockling scaling and parallel processing efficiency appear, as the downscaling sometimes reduces parallelism and increases processing time. The presenter stresses careful handling of GPU memory and resource cleanup to avoid accumulation and crashes.

---

#### [00:15:32 ~ 00:25:00] Debugging Scaling and Parallel Processing Bottlenecks  
Recent changes to scaling introduced performance regressions, causing slower processing and reduced parallelism. The team tests removing large PDFs from batches to isolate the issue. It appears that scaling reduces the number of parallel processes that can run simultaneously, leading to slower overall throughput. The presenter discusses the importance of understanding Dockling’s image extraction and scaling behavior. Dockling runs only once per document to extract images and layout elements, while resizing images happens outside of Dockling using Python libraries to avoid double processing and thread locking that would make operations sequential.

---

#### [00:31:04 ~ 00:41:07] Baseline Performance and Throughput Improvements  
The system is benchmarked at processing 138 to 166 pages per minute, a significant improvement from initial throughput of 8 pages per minute. The target is roughly 0.5 to 1 second to process each page, and this is being achieved using six concurrent workers. Documents vary widely in page count and complexity, with some having hundreds of high-quality pages and others being much smaller. The processing pipeline extracts tables, figures, formulas, and text chunks, with tens to hundreds of layout elements per document. GPU memory usage is carefully monitored, typically staying around 70-80 GB of VRAM, leaving room for additional concurrency.

---

#### [00:41:08 ~ 00:53:20] GPU Memory Accumulation and Cleanup Strategies  
A critical issue observed is the gradual accumulation of GPU memory usage with each batch request, which if unaddressed, could lead to out-of-memory crashes. The presenter identifies that some objects or states remain cached in GPU memory between requests. To mitigate this, the system implements explicit cleanup procedures to offload and free GPU memory after each document’s processing completes. This cleanup does not interfere with ongoing Visual Language Models (VLM) tasks, which reuse key-value caches (KV caches) for batching efficiency. The cleanup significantly stabilizes memory usage, allowing the system to sustain high throughput without crashing.

---

#### [00:53:46 ~ 01:05:00] Scaling Workers and Concurrency Optimization  
The team experiments with different numbers of Dockling workers (6, 8, 9, 10) and different concurrency levels to find the optimal balance between throughput and stability. They find eight workers to be a sweet spot, balancing GPU memory constraints and processing speed. Increasing beyond eight workers leads to memory saturation and crashes. The team also tweaks batch sizes for VLM requests, trying to increase from 128 to 256 or 512 chunks per forward pass, but memory and processing limits require careful tuning. Embeddings are currently processed sequentially, identified as a bottleneck, with plans to explore asynchronous or batched saving to optimize throughput further.

---

#### [01:11:25 ~ 01:28:19] Finalizing Throughput and Stability at 180 Pages per Minute  
The system stabilizes at around 180 pages per minute with eight concurrent Dockling workers and careful GPU memory management. The presenter confirms that retry logic for failed documents is functional but configured conservatively to avoid congestion. The system can process approximately 10,414 documents averaging 50 pages each in about 2.5 to 3 days. Larger or corrupted documents may fail and are isolated for manual or later processing. The presenter emphasizes the importance of monitoring GPU temperature, memory usage, and concurrency to maintain stability at scale.

---

#### [01:29:24 ~ 01:50:20] Architectural Insights and Future Improvements  
The presenter shares architectural lessons learned, including the need to separate CPU-bound and GPU-bound tasks, the challenges of using Dockling due to its threading and locking behavior, and the benefits of containerized microservices for scaling. They discuss image scaling strategies for high-resolution scanned documents and the trade-offs between quality and processing time. The presenter considers building a fully custom pipeline (potentially in Rust or C++) in future projects to avoid Dockling’s limitations. Plans include implementing dynamic scaling thresholds based on file size, improving embedding parallelism, and enhancing retry policies for failed documents.

---

#### [01:50:20 ~ 02:07:23] Deep Dive into Dockling Processing and Image Scaling  
Dockling extracts images and layout information once per document, with image resizing handled outside Dockling to avoid redundant processing. The architecture includes a CPU pass for initial pre-processing followed by GPU passes for layout and VLM inference. The presenter confirms that image scaling does not happen multiple times per document to maintain throughput. The pipeline is designed to avoid thread locks and sequential bottlenecks, enabling parallel processing of multiple documents. The current system achieves around 1.3 seconds per page on average with six workers, and throughput scales linearly with concurrency until GPU memory limits are reached.

---

#### [02:07:23 ~ 02:21:00] Embeddings Processing and Sequential Bottlenecks  
Embedding generation and saving are identified as sequential bottlenecks in the pipeline. Each document's embeddings are saved one after another, causing idle time on the GPU and slowing overall throughput. The presenter suggests researching asynchronous embedding generation and saving methods that maintain chunk integrity but allow concurrent processing. This is necessary to fully utilize the GPU and achieve higher throughput. The current embedding batch size is around 128 chunks per forward pass, with plans to increase it to 256 or 512 to improve throughput, pending GPU memory availability.

---

#### [02:21:00 ~ 02:40:21] Performance Monitoring and Memory Management  
Throughout the pipeline execution, GPU VRAM usage is closely monitored and maintained between 70-80 GB with occasional spikes up to 90 GB. The system employs memory cleanup after each document to prevent gradual memory leaks. The presenter highlights the importance of balancing concurrency, batch size, and memory usage to avoid crashes. There is acknowledgment that some documents, especially PowerPoint presentations or heavily image-dense PDFs, require specialized handling due to their unique structure. The overall architecture is modular and extensible for future improvements.

---

#### [02:40:21 ~ 03:14:07] Scaling Up and Saturation Points  
Increasing concurrency beyond eight workers leads to GPU saturation and memory errors, confirming the sweet spot for the current hardware and workload. The presenter explores increasing batch sizes for VLM requests to maximize GPU utilization while avoiding saturation. Testing indicates diminishing returns beyond certain concurrency and batch size thresholds. The system is designed to dynamically adjust processing parameters based on GPU memory availability to maintain efficiency. The presenter emphasizes iterative testing to find optimal configurations and plans for future automation of this tuning process.

---

#### [03:14:07 ~ 03:50:51] Handling Failures, Retries, and Long-Running Jobs  
The system includes robust retry logic for failed documents but avoids retrying failures immediately to prevent congestion. Instead, failed items are collected and retried separately or manually later. The presenter discusses using Tmux or Screen to run long processing jobs in detached sessions, allowing monitoring and resuming without interrupting ongoing processes. They recommend keeping a buffer of 5-7 GB of VRAM free to handle unexpected spikes and avoid crashes. The presenter shares insights on managing corrupted documents and maintaining state across job restarts.

---

#### [03:50:51 ~ 04:55:36] Final Throughput, Efficiency, and Next Steps  
The system consistently processes around 180 pages per minute with eight workers, translating to about 2.5 days to process 10,000 documents averaging 50 pages each. The presenter notes a roughly 90% reduction in processing time compared to initial naive implementations and highlights the impact of architectural improvements. They discuss potential future enhancements, including scaling to multi-GPU setups, using larger or more efficient models (e.g., FP8 quantization), and building more customized, thread-safe components to replace Dockling. Plans include developing domain-specific acronym extraction and RAG (Retrieval-Augmented Generation) agents to improve document querying.

---

#### [04:55:36 ~ 06:20:56] Wrap-Up, Live Production Run, and Community Interaction  
The presenter initiates the final production run of the document processing pipeline using Tmux for session management, enabling detachment and continued processing even if the stream ends. They confirm the system’s stability and throughput consistency during the run. The presenter thanks viewers for their support, briefly introduces the team, and announces plans to work on domain terminologies next to enhance the RAG agent’s capabilities. The session ends with reflections on the challenges faced during scaling, infrastructure design, and the value of open-source tools combined with custom engineering for large-scale document processing.

---

### Key Insights and Technical Highlights

- **Complex Document Handling:** NASA documents contain formulas, tables, graphs, and high-res images requiring specialized layout analysis beyond standard PDF chunking.
- **Single GPU Efficiency:** System achieves high throughput using a single NVIDIA H100 GPU with 95 GB VRAM by careful batching, concurrency, and workload separation.
- **Dynamic Image Scaling:** Adaptive downscaling based on file size helps manage large scanned documents, balancing detail retention and processing speed.
- **Separation of CPU/GPU Tasks:** The pipeline separates CPU-bound tasks (pre-processing, orchestration) from GPU-bound tasks (layout detection, VLM inference) to optimize resource usage.
- **Dockling Limitations:** Dockling’s threading model limits parallelism; workarounds include running multiple Dockling instances per document and external image resizing.
- **GPU Memory Management:** Explicit cleanup of GPU memory after each document prevents memory leaks and crashes, stabilizing long-running batch jobs.
- **Embedding Bottleneck:** Embedding generation and storage are currently sequential, representing a key target for asynchronous optimization to improve throughput.
- **Retry Handling:** Failures are expected (~5-10%), managed by deferred retries to avoid blocking active jobs.
- **Concurrency Tuning:** Eight concurrent Dockling workers provide the best balance between throughput and stability on available hardware.
- **Scalability:** Adding GPUs or upgrading models (e.g., larger parameter sizes, FP8 quantization) can further reduce processing time.
- **Infrastructure Design Lessons:** Custom thread-safe, lock-free pipeline components could significantly boost performance and scaling compared to off-the-shelf tooling.
- **Production Readiness:** The system can process 10,000+ complex documents in under 3 days, with monitoring and session management for reliability.
- **Future Directions:** Domain-specific acronym extraction, RAG agents, and embedding optimizations are planned to enhance functionality and user experience.

---

### FAQ

**Q: Why is Dockling a bottleneck?**  
A: Dockling uses a threading model that restricts parallel processing within a single instance, making multiple instances or custom solutions necessary for high throughput.

**Q: How does dynamic scaling work?**  
A: PDFs larger than configurable thresholds (e.g., 50 MB, 75 MB, 100 MB) are downscaled in image resolution by factors like 0.5 or 1.0 to reduce memory and processing overhead while maintaining readable quality.

**Q: How are failed documents handled?**  
A: Failed documents are collected and retried later or manually, avoiding retries during active batch processing to prevent GPU congestion.

**Q: What is the optimal concurrency level?**  
A: Eight Dockling workers currently provide the best tradeoff between speed and stability on a single H100 GPU with 95GB VRAM.

**Q: What is the average processing speed?**  
A: Approximately 180 pages per minute with six to eight workers, translating to about 2.5 days for 10,000 documents averaging 50 pages each.

**Q: How is GPU memory managed?**  
A: After processing each document, explicit cleanup frees GPU VRAM to prevent memory buildup and potential crashes, maintaining stable usage around 70-80 GB.

**Q: Are embeddings generated in parallel?**  
A: Currently, embeddings are generated and saved sequentially, causing a bottleneck. Research into asynchronous embedding processing is ongoing.

---

This detailed summary captures the full depth of the video stream content, highlighting the technical challenges, solutions, and ongoing optimizations in building a scalable, production-grade document processing system for complex NASA documents using limited GPU resources.


# [Domain-Specific Acronyms & Terminologies for 10K NASA docs | NASA thesaurus | Part 13](https://www.youtube.com/live/HuJmb1hfzQ4?si=mFqx1WA8zQ8D33WQ)
### Summary of Video Content: Building a Scalable RAG System for Aerospace Document Processing and Domain-Specific Terminologies

---

#### [00:00:03 ~ 00:04:38] Introduction to the Project and Current Status

- Raj introduces the ongoing project: building a production-grade Retrieval-Augmented Generation (RAG) system designed for handling aerospace documents. The system currently supports processing 10,000 documents but aims to scale to 85,000 to 100,000+ documents.
- The fictional company Meridian Aerospace is the client, dealing with diverse aerospace documents including proposals, test reports, safety analyses, failure investigations, component specifications, and regulatory filings, spanning several decades (1990s onward).
- The dataset is based on real NASA documents sourced from NASA's technical server, with approximately 10,000 documents already processed.
- The documents are complex, containing heavy technical jargon, images, mathematical formulas, graphs, and tables.
- The system employs large open-source models: a 7-billion to 8-billion parameter model for document layout detection (via Dockling) and a similar-sized model for document processing tasks such as generating descriptions, formatting tables, and handling markdown and formulas.
- Raj highlights the architectural setup where CPU workers run Dockling for layout detection, and GPU workers process embeddings and language models.
- Challenges faced with Dockling include threading and parallel processing issues, resulting in the deployment of multiple Dockling servers (around eight) and a batching system on the GPU side.
- The system processes about 120 pages per minute currently (down from 200 pages/minute initially), indicating slight performance degradation but stable progress.
- Raj explains the stateless worker pattern common in production ML systems, emphasizing how limited GPU resources (one H100 GPU) are efficiently utilized for large-scale document processing.

---

#### [00:04:38 ~ 00:14:59] Domain-Specific Acronyms and Terminologies: Motivation and Initial Setup

- A key focus of this session is domain-specific acronyms and terminologies (referred to as DTs), essential for aerospace documents.
- Raj stresses the importance of understanding why domain-specific terminologies matter for the system, particularly for improving retrieval accuracy and query understanding.
- The document processing pipeline is complete for the initial batch of documents, but the system is yet to fully integrate domain terminologies into the agent.
- Raj demonstrates launching the backend services, including the UI and embedding servers (4-billion parameter embeddings running with 4-bit quantization for efficiency).
- The UI is simple and allows interaction with the agent that is currently connected to a limited document collection for demonstration.
- Raj tests the system by sending queries and inspecting tool calls and the agent's ability to handle domain-specific questions.
- The agent can manage multiple tools: document search, updating nodes and tasks, section retrieval (e.g., parsing document sections like 2.3 or 2.5), and visual chunk inspection (taking screenshots of document pages or regions).
- The system uses customized pipelines for formulas, tables, and figures extraction, with fallback to visual inspection for difficult cases.
- Document metadata extraction is also part of the pipeline, capturing symbols, author info, document IDs, and creation dates—important for context and accurate retrieval.
- Raj shows how the agent can spawn sub-agents or research threads for parallel searching and deeper investigations, though nesting of sub-agents is limited to avoid recursion.
- The agent's UI supports notes and task management, helping to organize research workflows.
- Overall, the system is designed to be domain-aware, leveraging domain terminologies to enhance retrieval and understanding in a highly technical and jargon-heavy aerospace context.

---

#### [00:14:59 ~ 00:36:59] Why Domain-Specific Terminologies Are Crucial for Aerospace Document Search

- Raj discusses the critical problem of semantic retrieval failure when domain-specific acronyms are not recognized.
- Aerospace is a highly technical domain with many acronyms like "MMH" (Monomethylhydrazine), "NTO" (Nitrogen Tetroxide), "LOX" (Liquid Oxygen), and others that general language models or embedding spaces often fail to understand.
- Standard embeddings without domain adaptation lead to large semantic distances between queries and documents, causing retrieval failures even when the correct documents exist.
- The embedding space for 10,000 documents can produce around 800,000 to 1 million chunks (smaller text fragments indexed for search), making efficient and accurate retrieval a significant challenge.
- Raj uses a visual analogy comparing the embedding space to a geographic map where the goal is to narrow the search radius to a smaller, relevant subset of chunks rather than searching the entire space.
- Filtering by domain terminologies and metadata (such as document date or type) reduces the search space, improving precision.
- The aerospace domain has unique challenges: critical information like failure modes or anomaly sections can be only a few sentences in a long document but are vital for retrieval.
- Failure investigation reports are especially important and often cross-reference other documents, so the retrieval system must be capable of following references and understanding document linkages.
- Raj notes that legacy metadata in scanned or re-scanned documents may be inaccurate, adding complexity to the retrieval.
- He emphasizes that domain-specific acronyms, synonyms, and taxonomies must be incorporated into the retrieval system to improve recall and precision.
- Without domain knowledge, retrieval will fail on key aerospace queries involving pressure units (e.g., 2,000 PSI vs. 13.7 MPa) or specific technical jargon.
- Raj highlights that this problem is similar in other jargon-heavy domains like pharmaceuticals and legal documents.
- The system must handle synonyms, abbreviations, and various ways users may express technical terms.
- Raj references NASA's Domain Thesaurus (Disorders) dataset containing over 18,000 aerospace-related terms, synonyms, definitions, and hierarchical relationships (broader/narrower terms).
- This dataset is structured using SKOS (Simple Knowledge Organization System), a W3C standard for representing taxonomies and vocabularies in a machine-readable RDF format.
- Raj plans to leverage this thesaurus for query expansion and document enrichment without modifying the original document content.
- He points out that many companies lack centralized internal terminology documents, so some “tribal knowledge” remains unstructured and scattered.

---

#### [00:36:59 ~ 01:13:13] Implementation Details and System Performance

- Raj discusses integration plans to embed the domain terminologies into the system as vectors, enabling fuzzy matching and semantic search.
- The system will combine exact keyword matching with semantic embeddings to cover both acronym expansions and general meaning.
- He performs tests on embedding and indexing large batches of terms (e.g., 18,336 concepts with synonyms, broader/narrower terms).
- Raj also explores the trade-offs of including synonyms directly in embedding text, noting that it can slightly reduce embedding similarity for plain queries.
- The hybrid approach (combining exact matching on acronyms and semantic search on expanded terms) is preferred.
- Raj runs batch processing on his local machine (Apple M4 Pro, 24GB RAM) for embedding generation and indexing, noting the constraints compared to GPU-powered servers.
- He monitors GPU usage on a remote Nvidia H100 server running Dockling and embedding models, showing high utilization and batching optimizations.
- The document processing pipeline has processed over 1,600 documents (about 15% of the goal) with a failure rate of ~6.7%, which is acceptable given some corrupted or scanned documents.
- Page processing rate is about 104 pages per minute, expected to complete processing in 3-4 days.
- Raj mentions that the complex part isn’t just embedding but building an effective agent capable of handling 10,000+ documents with domain knowledge.
- He emphasizes that the retrieval system must find the “needle in the haystack” among hundreds of thousands to millions of chunks, requiring filtering by domain terminology and metadata.
- The system uses a combination of CPU and GPU workers, with multiple Dockling servers for layout detection and a batching system for embeddings and language model inference.
- Raj plans to write articles documenting key challenges and solutions in building large-scale document processing and retrieval systems.
- He clarifies that the NASA thesaurus data may be somewhat outdated but still useful for domain terminology.
- The SKOS structured vocabulary provides a solid foundation for building a domain terminology lookup service, including hierarchical relations and synonyms.
- Raj discusses the need for careful chunking to preserve critical context like anomaly descriptions in long documents.
- The system supports OCR for scanned and degraded-quality PDFs.
- The agent UI and backend include parallel search, task management, and note-taking features, mimicking a cloud code environment for multi-agent workflows.

---

#### [01:13:13 ~ 01:58:55] Domain Terminology Embedding and Query Expansion Strategy

- Raj downloads and processes the full NASA thesaurus dataset, loading 18,336 concepts with synonyms and hierarchical relations.
- He highlights the importance of storing these domain terminologies as embeddings, enabling fast fuzzy matching during query processing.
- The system supports injection of domain terminology expansions into the agent’s system prompt or as a separate tool that the agent can call on demand.
- Raj debates whether to inject terminology expansions directly into the system prompt (to influence every query) or provide it as a callable tool to reduce noise and hallucinations.
- The hybrid approach: lexical exact matching combined with semantic search is favored to handle acronyms and their expanded forms bidirectionally (e.g., user searches “LOX” or “liquid oxygen”).
- Raj confirms that including synonyms directly in embedding text can degrade pure semantic similarity, so multiple embeddings per concept might be necessary.
- He tests lookup speed, achieving sub-second (around 130 milliseconds) response times for term retrieval, suitable for real-time user experience.
- The system will parse user queries to extract key domain terms and perform parallel lookups on these terms before conducting document searches.
- Raj plans to limit domain terminology lookups to only when necessary (conditional tool calls), avoiding overhead on every query.
- The agent’s system prompt and tool invocation logic are designed to maintain domain intuition without overwhelming the model with noise.
- Raj writes a script to process and embed terminologies, storing them in a separate collection for efficient retrieval.
- He stresses the importance of concurrency and batching in embedding generation and query lookup to achieve millisecond-level latencies.
- Raj acknowledges that internal company acronyms and tribal knowledge are harder to capture without explicit documentation or additional workshops with domain experts.
- He summarizes the development process as iterative, with continuous refinement of indexing, embedding, retrieval, and agent logic.
- Raj notes that the entire project took about two weeks of intensive work, made possible by open-source models, and efficient GPU-CPU orchestration.
- He plans to document and share the architecture, challenges, and solutions in blog posts or Reddit for community benefit.

---

#### [01:58:55 ~ 03:07:44] Final Thoughts, Integration Plans, and Next Steps

- Raj finalizes the domain terminology embedding and search pipeline and prepares to integrate it with the agent.
- He emphasizes the importance of the agent only invoking domain terminology lookups when needed, to avoid unnecessary processing and reduce hallucinations.
- The system prompt and agent flow are designed to maintain a coherent context and domain intuition, ensuring smooth interaction.
- Raj plans to enable the agent to dynamically call the domain terminology tool as part of its reasoning process, enhancing query understanding.
- He documents the rationale behind the hybrid search approach and records decision points to maintain clarity in future development.
- Raj shows the concurrent processing architecture, including thread pooling and parallel embedding lookups.
- He discusses the importance of balancing exact keyword matches and semantic search for acronyms and expanded terms.
- Raj outlines the agent’s ability to spawn sub-agents or research threads, with limits to prevent runaway recursive calls.
- He notes that the system is stable and processing thousands of documents concurrently, with robust error handling and watchdog mechanisms to restart failed services.
- Raj encourages viewers to follow him on Twitter or Reddit for updates and plans to share detailed write-ups on building scalable document AI systems.
- He concludes the session by thanking viewers and indicating he will continue work on integrating domain terminologies and refining the agent.

---

### Key Insights and Takeaways

1. **Domain-Specific Terminologies Are Essential**: Aerospace documents contain numerous acronyms and jargon that generic language models and embeddings fail to capture, leading to poor retrieval results.

2. **Hybrid Search Approach**: Combining exact keyword matching with semantic embeddings provides better coverage of acronyms and their expanded forms, improving recall and precision.

3. **Large-Scale Document Processing Architecture**: Efficient orchestration of CPU-based layout detection with GPU-based embedding and language models allows scaling to tens of thousands of complex documents.

4. **Use of NASA’s Domain Thesaurus (Disorders)**: Leveraging an open-source, SKOS-structured thesaurus provides a rich foundation of domain knowledge for query expansion and document enrichment.

5. **Agent Design with Tool Calls and Sub-Agents**: The agent is designed to call domain terminology lookups as needed and spawn sub-agents for parallel research, improving robustness and flexibility.

6. **Preserving Document Context and Metadata**: Chunking strategies preserve critical context such as failure modes and anomaly sections, while metadata extraction helps filter and contextualize searches.

7. **Challenges with Legacy and Internal Terminologies**: Internal acronyms and tribal knowledge require additional strategies, such as workshops with domain experts and mining the corpus for frequently used terms.

8. **Performance Considerations**: Embedding lookups and query expansions must occur within milliseconds to maintain a responsive user experience, requiring efficient indexing and parallelism.

9. **Iterative and Documented Development Process**: The project progresses through phases of prototyping, testing, and refining, with detailed documentation to preserve design decisions and rationale.

---

### Keywords

- RAG System (Retrieval-Augmented Generation)
- Aerospace Document Processing
- Domain-Specific Terminologies (DTs)
- NASA Technical Documents
- Dockling (Layout Detection Framework)
- Embeddings, Semantic Search
- SKOS (Simple Knowledge Organization System)
- Query Expansion
- Hybrid Search (Exact + Semantic)
- Failure Investigation Reports
- Metadata Extraction
- Parallel Processing, GPU/CPU Orchestration
- Agent and Sub-Agent Architecture
- OCR for Scanned Documents
- Thesaurus / Domain Taxonomy
- Semantic Distance, Embedding Space Filtering
- Real-time Search Latency

---

### FAQ

**Q1: Why are domain-specific terminologies important?**  
A1: They capture acronyms and jargon unique to aerospace, which generic models fail to understand, causing poor retrieval accuracy.

**Q2: What is the role of NASA’s domain thesaurus?**  
A2: It provides structured vocabularies, synonyms, and hierarchical relations that improve semantic search and query expansion.

**Q3: How is the document processing pipeline architected?**  
A3: CPU workers handle layout detection with Dockling, while GPU workers run embedding and language models for content extraction and indexing.

**Q4: How does the system handle scanned or degraded documents?**  
A4: It uses OCR models and fallback visual inspection pipelines for formulas, tables, and figures.

**Q5: What is the hybrid search approach?**  
A5: It combines exact keyword matching (for acronyms) with semantic embeddings (for expanded forms and synonyms) to enhance retrieval.

**Q6: How is retrieval speed maintained at scale?**  
A6: By limiting the semantic search radius using domain filters and metadata, and through efficient parallel embedding lookups achieving sub-second latencies.

**Q7: Can the agent dynamically use domain terminologies?**  
A7: Yes, the agent can invoke a domain terminology lookup tool as needed, preventing unnecessary noise and hallucinations.

**Q8: What about internal company terminologies?**  
A8: These are often scattered as tribal knowledge; the system requires additional methods like workshops and corpus mining to extract them.

---

This detailed summary captures the technical depth, architectural design, challenges, and solutions addressed in Raj’s video stream on building a scalable aerospace document RAG system enhanced with domain-specific terminologies.


# [Domain Terminology & Semantic Search Optimization | Filtering 18K NASA Terms to 5.5K | Part 14](https://www.youtube.com/live/j0M5dDyLNPQ?si=F8Yeli-QJBpJj_vY)
### Summary of the Video Transcript on Building a Production-Grade Aerospace RAG System

---

#### [00:00:09 ~ 00:01:19] Introduction to the Project and Series Context  
The video begins by introducing Day 13 of a live series focused on building a **production-grade Retrieval-Augmented Generation (RAG) system** or an **agentic RAG system**. This system is designed to handle **85,000+ to 100,000+ aerospace-related documents**. The purpose of the system is to act as an intelligent search agent that can efficiently sift through thousands of complex documents to find relevant information, effectively serving as a domain-specific search engine and reasoning agent.

---

#### [00:00:44 ~ 00:02:46] Use Case and Document Nature  
The project revolves around a fictional aerospace consultancy called **Meridian Aerospace** with 180 employees. The company holds a vast archive of aerospace documents, including internal research papers, NASA and SpaceX documents, technical reports, safety analysis, failure investigation reports, and other materials spanning multiple decades, sometimes going back to the 1950s. These documents are complex, often scanned, handwritten, or lacking metadata.

A critical pain point is engineers spending **4 to 6 hours per project** searching through archives for relevant historical test data and failure modes. Institutional knowledge is often locked in senior engineers who are retiring, creating risks such as missing critical failure modes during safety reviews. The dataset contains **very old, jargon-heavy aerospace documents** with a significant percentage (40%) being scanned copies requiring OCR.

---

#### [00:03:12 ~ 00:05:40] Technical Challenges and Current Progress  
The project has tackled numerous challenges, including:

- **OCR and visual language models (VLMs)** for scanned documents.
- Handling **heavy aerospace jargon** with domain-specific acronyms and synonyms that evolve over decades (e.g., "chamber combustion" vs. "stability combustion").
- Managing **18,414 embedded domain terminologies** to improve search accuracy.
- Processing **formulas, tables, technical diagrams, and images** within documents.
- Building a hybrid search system combining **keyword and semantic search** with sub-240 millisecond latency.
- Infrastructure challenges of processing 10,000+ documents on a **single NVIDIA H100 GPU**, achieving about 110 pages per minute sustained throughput despite GPU and RAM bottlenecks.

The speaker emphasizes that this system, while fictional, represents a realistic and highly valuable aerospace RAG project worth around $70,000 to $250,000 in real-world terms.

---

#### [00:06:13 ~ 00:08:43] System Processing Metrics and Document Characteristics  
At this point, the system has processed around **5,500 documents out of 10,400**, with a **17% failure rate** that is being addressed via retries. The total processing time has exceeded **36 hours**. Documents are large, averaging **67 pages each**, containing dense technical content, formulas, and images.

The document processing pipeline was custom-built for accuracy, leveraging **layout detection tools (Dockling)** and specialized methods for **noise removal** (e.g., stripping confidential statements) to ensure the model focuses on relevant text and visuals.

---

#### [00:11:08 ~ 00:13:22] Model and Infrastructure Details  
The backend uses a **7-8 billion parameter language model (Qwen-8B)** quantized to **FP8** precision to optimize GPU memory usage on the H100. The system batches queries efficiently, processing up to 256 requests per forward pass, which aligns with how large-scale cloud models serve millions of users simultaneously.

The speaker explains how batching works in production systems to optimize GPU usage and latency, noting that user queries are not processed sequentially but in batches that may introduce slight variable latency depending on batch fullness.

---

#### [00:17:01 ~ 00:19:26] Challenges with Dockling and Multi-Server Setup  
Dockling layout detection servers are limited to 8 concurrent threads due to internal constraints, causing some bottlenecks. The system uses **watchdogs** to monitor these servers and restart failed processes within seconds, ensuring robustness. The speaker reflects on the trade-offs between using cloud GPUs like H100s and alternatives like B200 GPUs for cost and speed optimization.

---

#### [00:19:30 ~ 00:23:41] Demo of Agent Interface and Domain-Specific Querying  
The speaker demonstrates a simple chatbot UI powered by Claude’s skills pack, allowing queries into the processed aerospace documents. The agent supports adjacent chunk navigation, image viewing, formula verification, and task management. A notable feature is the integration of the **NASA Thesaurus V2**, a standardized aerospace domain terminology database, which enables the agent to understand complex domain jargon and synonyms, critical for accurate search and reasoning.

---

#### [00:23:39 ~ 00:32:43] Importance and Challenges of Domain Terminologies  
The NASA thesaurus contains over 18,000 aerospace domain terms, including acronyms like **LOX** (liquid oxygen), **NTO**, and other propulsion-related terms. The agent uses this terminology to expand and refine queries, handling unit conversions and evolving terminology over decades (e.g., PSI vs. MPa).

The speaker highlights the difficulty of making the agent consistently use domain terminologies during query processing, especially when the user’s input already contains precise jargon. They note that fine-tuning or explicitly injecting these terminologies into the model prompt or tool calls may be inefficient or unnecessary if the model already understands these terms.

---

#### [00:32:43 ~ 01:00:03] Experiments with Domain Terminology Tool and Model Behavior  
Through testing, the agent sometimes ignores the explicit **domain terminology lookup tool** when the query is clear, relying on its internal knowledge. When queries are vague, the terminology tool helps expand relevant keywords and synonyms.

The speaker suggests that for open-source or smaller models with less domain knowledge, the terminology tool is more critical. However, for large models like Claude, the impact is more subtle. They also emphasize the need to filter out noise terms (such as medical terminology irrelevant to aerospace) to improve search precision.

---

#### [01:00:03 ~ 01:15:39] Filtering and Refining Domain Terminologies  
Because the NASA thesaurus includes many terms outside the propulsion domain (e.g., medical terms), the speaker undertakes a filtering step to reduce the 18,000+ terms to around 3,500 **propulsion-related domain-specific terms**. This pruning reduces noise and improves semantic search accuracy.

They discuss the limitations of embedding models on very short texts or keywords and advocate for a hybrid approach combining **keyword matching** with **augmented semantic search**, particularly for short domain-specific phrases.

---

#### [01:18:25 ~ 01:26:55] Handling Document Updates and Data Ingestion  
The speaker answers a viewer question about managing document updates and deletions in the database. They describe a workflow where:

- Incoming documents are filtered and metadata-extracted.
- Similarity searches identify draft or production versions.
- Metadata includes dates and versioning to manage relevance.
- Small models or agents help identify document relationships.
- Manual or semi-automated pipelines are needed due to domain complexity.

They emphasize no one-size-fits-all solution exists, and each domain requires tailored heuristics.

---

#### [01:26:55 ~ 01:39:36] Finalizing Domain Terminologies and Agent Testing  
After filtering and augmentation, the agent performs better in pulling relevant aerospace propulsion terms and synonyms during search. The speaker notes that the model filters noise intelligently and only uses domain terminology when contextually relevant.

They finalize the domain terminology tool integration and confirm the current system is stable, scalable, and ready for large-scale deployment.

---

#### [01:41:05 ~ 01:58:56] Document Chunking, Metadata, and Search Strategy  
The agent works with over **800,000 chunks** of document data derived from roughly 5,000 documents. Each chunk contains rich metadata, including section headings and document structure, enabling the agent to navigate document hierarchies effectively.

The speaker explains their chunking strategy:

- Initially chunking by paragraphs, which sometimes causes uneven chunk sizes.
- Considering setting minimum chunk sizes (~256 tokens) for more consistent processing.
- Leveraging metadata to link chunks by section for coherent retrieval.

The search strategy involves:

- Conducting a **parallel keyword search** across the large chunk corpus to identify relevant “locations” in the document space.
- Then expanding contextually from these hits to gather adjacent information.
- Mimicking how engineers narrow down documents by first finding relevant sections before deep reading.

---

#### [02:00:14 ~ 02:20:43] Agent Simulation, User Behavior Modeling, and Evaluation Framework  
The speaker outlines their approach to modeling user behavior and agent reasoning via **simulations**:

- Creating **personalities** representing junior and senior engineers with domain experience.
- Running these personalities through typical workflows to understand their queries and thought processes.
- Using these insights to craft **system prompts** that make the agent behave like an aerospace engineering consultant, not just a search engine.
- Emphasizing the importance of a carefully designed **system prompt** to embed domain knowledge and reasoning heuristics rather than relying solely on tool complexity.

For evaluation, they plan to:

- Select around **20-30 documents** as an evaluation subset.
- Load these into a large LLM with 1 million token capacity (e.g., Gemini) for reference answers.
- Compare the agent’s ability to find the relevant documents within the full 5,000+ document corpus.
- Identify gaps and iterate on agent design accordingly.

---

#### [02:39:43 ~ 03:15:38] Ongoing Work, Chunking Issues, and Next Steps  
The speaker resumes work on integrating the current system with AI Studio and preparing for evaluation:

- Highlights the importance of **landscape analysis** and **multi-resolution search** to deal with document distribution and chunk similarity.
- Plans to create a **data set of 25 full documents** saved in order for coherent evaluation.
- Notes chunking granularity issues, particularly overly small chunks, and plans to merge or adjust chunk sizes without breaking document order.
- Estimates around **200,000 tokens** currently in the evaluation set, which Gemini or similar LLMs can handle.
- Confirms the infrastructure is stable with backups and snapshots to avoid data loss.

---

#### [03:18:07 ~ 03:19:02] Conclusion and Upcoming Focus  
The video concludes with a summary stating that:

- Document processing and indexing are largely complete.
- The focus will shift to **evaluation and identifying gaps** in the agent’s performance.
- The system is complex but stable, and the next phase involves rigorous testing and refinement.
- The speaker thanks viewers and encourages further questions and interaction.

---

### Core Concepts and Takeaways

- **Large-scale document ingestion:** Handling 10,000+ aerospace documents with mixed formats (scanned, handwritten, digital).
- **Domain-specific knowledge:** Embedding 18,000+ aerospace terminologies, filtered to 3,500 propulsion-specific terms, to improve search accuracy.
- **Hybrid search strategy:** Combining keyword matching and semantic search with efficient indexing (Quadrant DB).
- **Model optimization:** Using quantized large language models (7-8B parameters at FP8) for cost-effective GPU usage on a single H100.
- **Chunking and metadata:** Intelligent chunking by paragraph with section metadata aids navigation and retrieval.
- **Agent design via simulation:** Creating user personas and workflows to craft system prompts tailored to aerospace domain reasoning.
- **Evaluation methodology:** Using a subset of documents loaded into a large LLM for ground truth generation, comparing agent retrieval performance.
- **Infrastructure robustness:** Multi-server setup with watchdogs, batching techniques, and backups to ensure continuous processing.

---

### Keywords

- Retrieval-Augmented Generation (RAG)
- Aerospace documents
- Domain terminology embedding
- Hybrid semantic and keyword search
- Document chunking and metadata
- Large language models (LLMs)
- FP8 quantization
- NASA Thesaurus
- Agent simulation and system prompt engineering
- Evaluation framework with large LLMs
- GPU batching and infrastructure monitoring

---

### FAQ

**Q: Why is domain terminology important in aerospace document search?**  
A: Aerospace documents contain highly specialized jargon, evolving acronyms, and unit variations. Without domain terminology integration, the search system cannot reliably retrieve relevant documents or interpret queries accurately.

**Q: How does the system handle scanned and handwritten documents?**  
A: The system uses OCR combined with visual language models and layout detection tools like Dockling to extract text, formulas, tables, and images from complex scanned documents.

**Q: What is the role of simulations in agent design?**  
A: Simulations model different user personas and their workflows, helping craft system prompts that guide the agent’s reasoning to behave like domain experts, improving relevance and usability.

**Q: How is document update and versioning managed?**  
A: By extracting metadata and using small models or agents to detect document relationships and versions, the system can identify drafts versus production files and update the database accordingly.

**Q: What are the main bottlenecks in processing large document corpora?**  
A: GPU memory constraints, thread limitations in layout detection tools, and variability in chunk sizes pose challenges that require batching, monitoring, and efficient pipeline design.

---

This detailed summary captures the essential content, technical depth, and project progress described in the video transcript, neatly structured following the original timeline and themes.


# [End to End: 10K Docs Indexed, Agent Reasoning Across 50 Years, Evaluation with Gemini | Part 14](https://www.youtube.com/live/WT6KWo_eqyI?si=3aAEN0aSgQxnsKrK)

### Summary of Video Content: Building a Production-Grade System for NASA Documents

- **[00:00:05 ~ 00:02:07] Introduction and Project Overview**  
  The project involves building a scalable, production-grade AI system designed to process and analyze over 10,000 NASA technical documents, with the capability to scale beyond 85,000 and even 100,000 documents. These documents span from as early as the 1950s (specifically the 1951 document is mentioned) through to 2025. They are complex, containing dense technical jargon, diagrams, formulas, tables, and scanned copies from different eras. The data source is NASA Technical Reports Server (NTRS), which is freely accessible, allowing bulk document downloads with some rate limits. The project aims to assist aerospace engineers by drastically reducing the hours they spend searching through archives and help surface relevant documents and detailed information efficiently.

- **[00:02:34 ~ 00:04:42] Document Processing Pipeline and Challenges**  
  The system is built for a fictional midsize aerospace engineering consultancy called Meridian Aerospace, which handles safety certifications, propulsion systems, and satellite technologies for government and commercial clients. Engineers typically spend four to six hours per project searching through documents. The system’s goal is to enable semantic search and rapid retrieval across a massive archive. The documents include scanned copies with complex layouts, tables containing formulas, images, and diagrams. The team spent several days (3-4 days over multiple live streams) developing a custom document processing pipeline that goes beyond basic chunking: it has specialized pipelines for formulas, diagrams, tables, mathematical equations, and figures. Noise such as blacked-out classified data is cleaned. Layout detection is performed using Dockling, and open-source large language models with approximately 7 billion parameters are used for embedding and analysis.

- **[00:04:43 ~ 00:06:52] Scaling and Infrastructure**  
  Processing 10,000 documents took about two days using a single NVIDIA H100 GPU. Approximately 20% of documents initially failed processing, but retries are planned. The processed data contains about one million embedding chunks, representing a significant scale challenge. The infrastructure combines CPU and GPU layers with parallel processing and watchdog monitoring to ensure reliability. The team encountered issues such as unexpected restarts causing data loss but mitigated this by taking snapshots of the processed data. The system currently holds about 8,000 to 9,000 successfully processed documents in the vector database (Quadrant).

- **[00:06:18 ~ 00:09:48] Intelligent Agent Design and Domain-Specific Terminology**  
  An intelligent agent, designed to mimic a human researcher, was built over 3-4 days. This agent uses domain intuition and several tools to interact with the document database, including navigating document sections, retrieving specific chunks, and parallel research capabilities. It supports complex technical queries with domain-specific jargon. About 18,000 jargon terms and their synonyms were collected from the aerospace and life sciences domains. Instead of fine-tuning a model, the team integrated this jargon as a tool to improve understanding. The system emphasizes filtering jargon and embedding only a subset (4,000-5,000) relevant to propulsion documents to optimize performance. The current phase focuses on final polishing and resolving outstanding issues before project completion.

- **[00:09:39 ~ 00:19:58] Chunking and Embedding Optimizations**  
  A major issue identified was the chunk size during document processing. The system used Dockling’s default paragraph-level chunking, which sometimes produced very small chunks (e.g., headings or tiny text snippets). This caused inefficiencies in embedding and retrieval, as many chunks were too granular. The minimum chunk size was set around 150 tokens, but the ideal would be around 512 tokens to improve context and relevance in search queries. The team discussed options:  
  - Reprocessing documents with larger chunk sizes (costly due to compute time of 40-50 hours).  
  - Merging small chunks post-processing without reprocessing the entire document.  
  - Applying filters to ignore chunks below a size threshold during retrieval.  
  The preferred solution was to create a new collection by merging existing small text chunks into larger ones, preserving document order and metadata (such as section headers). Special care would be taken to avoid merging non-text chunks like tables, images, or formulas. The goal is to improve relevance by having more meaningful chunks, not necessarily longer ones. This approach would preserve computational resources while enhancing retrieval quality.

- **[00:20:52 ~ 00:25:59] Metadata and Section Headers Handling**  
  The merging procedure must carefully handle metadata such as section headers and document structure, as merging chunks across different sections could confuse context. The system stores section header metadata alongside the text chunks, which allows informed merging that respects document boundaries. The order of chunks is crucial and should be maintained to keep the integrity of the document’s narrative. The team planned to test merging with chunk size targets of minimum 512 tokens and maximum up to 2,000 tokens, balancing chunk size for context while avoiding excessively large embeddings.

- **[00:29:26 ~ 00:41:50] Processing Implementation and UI Improvements**  
  The merging process was implemented as a dry run, and the team discussed the expected runtime and resource usage. The collection would be duplicated using snapshots to ensure safety and rollback capability if errors occurred. Parallel processing was planned to speed up merging.  
  Meanwhile, UI issues were addressed, such as fixing rerendering problems in the “sources” panel, which displays the provenance of answers to build user trust. The system was tuned to handle large embedding computations and slowdowns typical with large datasets.

- **[01:04:49 ~ 01:22:34] Handling Image and Formula Rendering**  
  A significant feature is the handling of images and formulas extracted from scanned documents. The agent can request visual regions or images of diagrams, tables, or formulas to verify its textual understanding and provide richer context to users.  
  Challenges included serving images stored on a VM while the API runs on the local machine. The team planned to implement an image-serving API that returns Base64-encoded images to the frontend for inline rendering. This API would handle requests for images, figures, and formulas, enabling the user to view these directly in the UI alongside text responses.  
  The agent supports viewing regions of PDFs or images, improving the user experience by integrating visual verification into the research workflow.

- **[01:37:56 ~ 01:58:17] Snapshot and Data Backup Strategy**  
  To prevent data loss during reprocessing or system failures, snapshots of the entire document processing state were created on Azure. These snapshots allow quick restoration without needing to re-download or reprocess large document sets.  
  The team emphasized the importance of slow, cautious operations when working with large datasets and complex pipelines to avoid costly mistakes or data loss.

- **[02:15:59 ~ 03:04:01] Validating Image and Formula Retrieval**  
  The system was tested with queries for rocket images, propulsion diagrams, and formulas. The agent successfully retrieved and displayed relevant images and formula regions, demonstrating the end-to-end processing and retrieval pipeline works correctly for complex visual data in documents.  
  The UI shows thumbnails of images the agent “sees” and enables users to click and expand them. Verification of formula extraction accuracy was tested with multiple formulas, with a success rate of about 90-95% accuracy.

- **[03:10:56 ~ 04:10:53] Domain Reasoning and Search with Temporal Filtering**  
  The system supports filtering documents by creation year, enabling time-bounded searches (e.g., finding all relevant documents from the 1970s or 2020s). This is critical for aerospace research where historical context matters.  
  Challenges included missing metadata for document creation years due to earlier processing errors. The team developed backfill scripts to extract year data from document numbering schemes and update the metadata in the vector database, enabling efficient numeric filtering using Quadrant’s payload indexing.  
  This filtering dramatically reduces search space and improves retrieval speed and relevance.  
  The system also understands cross-document references, enabling the agent to follow citation trails or related reports, which is crucial for aerospace research workflows.

- **[04:11:54 ~ 04:38:15] Timeline-Based Research and Evolution of Technologies**  
  The agent was able to synthesize historical timelines of technological evolution in cryogenic propellant systems, summarizing key advancements from the 1970s to the 2020s. It identified major shifts such as from passive insulation to active cryocoolers and autonomous operation.  
  This shows the system’s ability to aggregate knowledge across decades of research documents, providing valuable insights into technological progress and research trends.

- **[04:43:59 ~ 06:00:00] Evaluation Framework and Testing Scenarios**  
  The project moved into a robust evaluation phase, testing the system’s ability to retrieve relevant documents from a large corpus (10,000+ documents) and answer complex aerospace engineering questions.  
  Evaluation scenarios covered:  
  - Retrieval accuracy: finding the correct documents among thousands.  
  - Domain reasoning: interpreting technical content and jargon.  
  - Handling degraded documents: OCR errors, scanned tables, and images.  
  - Negative boundary cases: recognizing when information does not exist and avoiding hallucinations.  
  - Cross-referencing: linking related documents for comprehensive answers.  
  The system was tested with multiple real-world-like questions involving technical details, formulas, and diagrams. It successfully retrieved relevant documents, extracted numerical data, and provided references. The agent’s ability to autonomously search related documents and triangulate answers was highlighted as a key strength.

- **[06:00:00 ~ 07:15:57] Final Results, System Strengths, and Project Reflections**  
  The evaluation showed the agent achieving around 80-100% accuracy on different scenarios, with better results on more advanced models (e.g., Sonet outperforming Haiku).  
  The system can handle 85,000+ documents and scale to 100,000+ with proper infrastructure. Processing time for 10,000 documents was about 46 hours on an H100 GPU.  
  The project required sophisticated document processing, including handling technical jargon, diagrams, tables, OCR errors, and metadata extraction.  
  The system’s trustworthiness is enhanced by showing source documents and images inline, allowing users to verify answers.  
  The team emphasized the importance of domain understanding, user workflows, and integration with existing enterprise systems.  
  The project cost (compute, time, licensing) was estimated around $5,000 monthly for GPU rentals, with potential commercial value of $100,000-$200,000 for enterprise deployment.  
  The speaker reflected on the challenge and novelty of building such a system from scratch, highlighting the absence of one-size-fits-all solutions, and the necessity of domain-specific approaches.  
  A commercial product, “Intrlex,” was introduced as a 100x more powerful, on-premise, scalable enterprise search system for regulated and classified documents in aerospace, finance, pharma, and other domains requiring compliance.

- **[07:07:00 ~ 07:16:07] Closing Thoughts and Advice**  
  The project showcased the full lifecycle of building a production-grade document AI system at scale for a highly technical domain.  
  The speaker encourages creativity, experimentation, and understanding user needs deeply rather than following rigid patterns.  
  The system architecture involves complex interplay between document processing, embedding, metadata, agent design, and UI/UX considerations.  
  The speaker invites feedback, questions, and collaboration, promising future articles and code to help others build similar systems.  
  The entire journey took over two weeks of intensive work, including multiple days of live streams, and involved solving many infrastructure and technical challenges.

---

### Key Insights and Technical Highlights

- **Scalability & Infrastructure**: Processing 10,000+ documents with millions of chunks requires robust GPU and CPU orchestration, parallel processing, and fault tolerance with snapshot backups.

- **Document Processing Complexity**: Handling scanned documents with formulas in tables, images, and technical diagrams requires custom pipelines beyond naive chunking.

- **Chunking Strategy**: Optimal chunk size (target ~512 tokens) is critical for embedding quality and retrieval relevance; post-processing chunk merging can avoid costly recomputation.

- **Domain Expertise & Jargon**: Aerospace documents contain 18,000+ technical jargon terms; integrating domain-specific terminology as tools improves comprehension without expensive fine-tuning.

- **Temporal Filtering & Metadata**: Extracting document creation year and supporting numeric range filters significantly improves search precision.

- **Cross-Document Reasoning**: The agent can follow references and citations to assemble comprehensive and accurate answers.

- **Visual Data Handling**: Serving images and formulas inline via Base64 encoding enhances trust and usability, allowing users to verify extracted data.

- **Evaluation Framework**: Multi-dimensional testing including retrieval accuracy, cross-reference navigation, degraded document robustness, domain reasoning, and hallucination control.

- **High Accuracy Achieved**: Achieved near 90-100% accuracy on complex aerospace document queries in a corpus of 10,000+ documents.

- **Commercial Viability**: Projected enterprise value $100k–$200k; with scalable on-premise solutions like Intrlex for highly regulated environments.

---

### Recommended Testing & Evaluation Aspects

- Retrieval accuracy: Does the system find the correct documents in a large corpus?  
- Domain reasoning: Can the system interpret technical jargon and complex concepts correctly?  
- Handling degraded documents: Does it cope with OCR errors and noisy scanned data?  
- Cross-document navigation: Can it track references and related documents?  
- Negative boundary queries: Does it correctly respond when information is missing without hallucination?  
- Speed and scalability: How fast is retrieval and response with increasing document counts?  
- User trust: Are sources and images presented clearly to verify answers?

---

### Conclusion

This video documents an end-to-end journey of building a highly specialized, scalable AI system for aerospace document search and analysis, addressing unique domain challenges with innovative pipelines, agent design, and evaluation strategies. The system demonstrates high accuracy and robustness, making it suitable for deployment in demanding research environments with large, complex document archives. The project also emphasizes the importance of domain understanding, user workflow integration, and iterative evaluation to deliver a valuable product.



# Keywords
- RAG (Retrieval-Augmented Generation)
- Aerospace Documents
- Semantic Search
- Multimodal AI (VLM)
- Document Parsing
- Dockling
- Vector Database (Quadrant)
- Domain Terminology Embeddings
- Confidence Scoring
- Table Extraction
- Formula Extraction
- On-Premise AI Deployment
- NASA Documents
- AI Agent Design
- Domain Expert Personas
- Rocket science documents
- Aerospace documents
- Table extraction
- Vision language models (VLM)
- Heat map boundary detection
- Zebra striping
- Document chunking
- Metadata extraction
- Report documentation page
- Symbols and abbreviations
- Formula extraction
- Semantic search
- On-prem AI system
- Open-source AI models
- Document layout detection
- Document indexing
- Technical document understanding
- Document processing pipeline
- Multi-page tables
- Contextual image extraction
- Retrieval-Augmented Generation (RAG)  
- Document Chunking  
- Formula Extraction  
- Bounding Box Visualization  
- Vision-Language Model (VLM)  
- Dockling  
- Inline Math  
- Semantic Search  
- Embedding Models  
- Quadrant Vector DB  
- Prompt Engineering  
- Noise Filtering  
- Aerospace Documents  
- Open Source AI Models  
- Agent-Based Verification  
- Document Ordering  
- Metadata Enrichment  
- GPU Parallelization  
- Model Quantization  
- Technical Document Processing  
