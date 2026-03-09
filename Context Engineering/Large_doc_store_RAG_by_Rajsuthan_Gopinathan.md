
## [PART 1 - Building a Scalable RAG System for Rocket Science Documents](https://www.youtube.com/live/bkKVWf7qQUk?si=YL2UrWcjZH18B9SZ)
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


### [Formula Extraction, Visual Anchoring and more for NASA docs from 1960s | NASA RAG | Part 3 ](https://www.youtube.com/live/1do7SXZ12dk?si=sKqO8D4GCLNLtknB)
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



### Keywords
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
