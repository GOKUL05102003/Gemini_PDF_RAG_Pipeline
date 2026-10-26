# Gemini PDF RAG Pipeline

This project is a Retrieval-Augmented Generation (RAG) pipeline built entirely in Python using Google's Gemini API, ChromaDB, and PyPDF. It allows users to upload a PDF document, process its text into searchable vector embeddings, and query the document using natural language to get precise, context-aware answers.

## Features
* **PDF Text Extraction**: Parses raw text from PDF documents using `pypdf`.
* **Local Vector Storage**: Utilizes `ChromaDB` for ephemeral, local vector storage without relying on external cloud databases.
* **Google Gemini Embeddings**: Leverages the `gemini-embedding-001` model to create high-quality semantic vectors of document chunks.
* **Context-Aware QA**: Uses the `gemini-3.5-flash-lite` model to generate accurate answers based *strictly* on the retrieved document context.

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
1. **Install Dependencies**: Installs `pypdf`, `chromadb`, and `google-generativeai`.
2. **Configure API**: Automatically retrieves and configures your Gemini API key from Colab Secrets.
3. **Upload PDF**: A file prompt will appear. Select any PDF (e.g., a corporate policy, financial report, or environmental summary) to analyze.
4. **Extract & Chunk**: The code extracts the text and splits it into overlapping chunks to preserve semantic meaning.
5. **Initialize & Embed**: The text chunks are embedded and loaded into a local ChromaDB collection in throttled batches to respect API rate limits.
6. **Query the Document**: Scroll to the final step, type your question into the text box, and run the cell to retrieve a context-backed answer.

## Technologies Used
* [Google Generative AI SDK](https://github.com/google/generative-ai-python)
* [ChromaDB](https://www.trychroma.com/)
* [PyPDF](https://pypdf.readthedocs.io/)
* Google Colab