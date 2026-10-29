# LangChain RAG Pipeline with Gemini & ChromaDB

This project is a Retrieval-Augmented Generation (RAG) pipeline built using **LangChain**, Google's **Gemini API**, **ChromaDB**, and **PyPDF**. It allows users to upload a PDF document, process its text into searchable vector embeddings, and query the document using natural language to get precise, context-aware answers.

## Why LangChain? (Advantages over Native SDKs)
Transitioning this project to LangChain provides several architectural and developmental advantages:
* **Advanced Text Chunking:** Instead of writing custom Python logic for chunking, LangChain's `RecursiveCharacterTextSplitter` intelligently splits text based on natural boundaries (paragraphs, sentences) rather than arbitrary character counts, preserving semantic meaning much better.
* **Rich Document Metadata:** LangChain's `PyPDFLoader` automatically extracts and attaches metadata (like page numbers) to each document chunk. This allows the system to cite exactly which page an answer came from.
* **Declarative Pipelines (LCEL):** LangChain Expression Language (LCEL) allows the RAG chain to be composed elegantly using a readable pipeline syntax (`retriever | prompt | llm | parser`), making the code easier to debug and scale.
* **Component Modularity:** Because LangChain acts as an abstraction layer, switching the vector database (e.g., from Chroma to Pinecone) or the LLM (e.g., from Gemini to OpenAI) requires changing only one or two lines of code, preventing vendor lock-in.

## Features
* **PDF Text Extraction**: Parses raw text and page metadata using `PyPDFLoader`.
* **Local Vector Storage**: Utilizes `langchain-chroma` for ephemeral, local vector storage without relying on external cloud databases.
* **Google Gemini Embeddings**: Leverages the `GoogleGenerativeAIEmbeddings` wrapper (`gemini-embedding-001`) to create high-quality semantic vectors.
* **Context-Aware QA**: Uses the `ChatGoogleGenerativeAI` model (`gemini-3.5-flash-lite`) integrated into an LCEL chain to generate accurate answers based *strictly* on retrieved context.

## Prerequisites
To run this project, you will need:
* A Google account to use [Google Colab](https://colab.research.google.com/).
* A **Google Gemini API Key**. You can get one from Google AI Studio.

## Setup Instructions

1. **Open in Google Colab**: Upload the `RAG.ipynb` notebook to Google Colab.
2. **Configure API Key**: 
   * In Google Colab, click on the "🔑 Secrets" tab on the left sidebar.
   * Add a new secret with the Name: `GEMINI_API_KEY` and paste your API key in the Value field.
   * Toggle the button to allow notebook access to the secret.
3. **Hardware Acceleration** (Optional but recommended): Go to `Runtime` > `Change runtime type` and select `T4 GPU` for faster processing.

## Usage Guide

Run the notebook cells sequentially:
1. **Install Dependencies**: Installs the `langchain` ecosystem, `pypdf`, `chromadb`, and `langchain-google-genai`.
2. **Configure API**: Automatically retrieves and configures your Gemini API key from Colab Secrets.
3. **Upload PDF**: A file prompt will appear. Select any PDF (e.g., a corporate policy or environmental report) to analyze.
4. **Extract & Chunk**: The `PyPDFLoader` and `RecursiveCharacterTextSplitter` parse and intelligently chunk the document.
5. **Initialize & Embed**: The text chunks are embedded and loaded into a local ChromaDB collection in throttled batches to respect API rate limits.
6. **Build & Query the Chain**: The LCEL RAG chain is constructed. Type your question into the text box and run the final cell to retrieve a context-backed answer, complete with page number citations.

## Technologies Used
* [LangChain](https://www.langchain.com/) (Core, Community, Core-GenAI integrations)
* [Google Generative AI](https://ai.google.dev/)
* [ChromaDB](https://www.trychroma.com/)
* [PyPDF](https://pypdf.readthedocs.io/)