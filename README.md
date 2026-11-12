# PDF AI Assistant — Hybrid RAG

An AI-powered PDF question-answering assistant that combines semantic search, keyword retrieval, and cross-encoder reranking to provide context-grounded answers with page-level citations.

## Project Overview

This project allows users to upload a PDF document and ask questions about its content. It retrieves relevant passages using a hybrid retrieval pipeline and generates answers grounded in the uploaded document.

The system is also designed to abstain when the requested information is not available in the document.

## Architecture

1. **PDF Extraction:** Extracts text while preserving page information using PyPDF.
2. **Text Processing:** Cleans and splits text into sentence-aware chunks.
3. **Semantic Retrieval:** Generates embeddings using OpenAI `text-embedding-3-small` and indexes them with FAISS.
4. **Keyword Retrieval:** Uses BM25 to retrieve relevant passages based on keyword matching.
5. **Hybrid Retrieval:** Combines semantic and keyword results using Reciprocal Rank Fusion (RRF).
6. **Reranking:** Uses `BAAI/bge-reranker-v2-m3` to rerank retrieved passages.
7. **Answer Generation:** Uses GPT-4o-mini to generate answers grounded in retrieved context.
8. **Citations:** Provides page-level references in generated answers.
9. **Evaluation and Logging:** Includes retrieval tests, answer checks, citation checks, abstention tests, and JSONL interaction logging.
10. **User Interface:** Provides an interactive Gradio interface.

## Technologies

- Python
- OpenAI API
- FAISS
- BM25
- Sentence Transformers
- Cross-Encoder Reranking
- Gradio
- PyPDF

## Evaluation

Tested on a sample PDF document using a small evaluation dataset.

| Evaluation | Result |
|---|---:|
| Page-level Recall@4 | 5/5 |
| Evidence phrase matching@4 | 5/5 |
| Expected answer fact checks | 6/6 |
| Expected page citation checks | 6/6 |
| Abstention test | 1/1 |

These results represent checks on a small test dataset and should not be interpreted as general model accuracy or independently verified citation accuracy.

## Limitations

- PDF text extraction may be unreliable for scanned documents, complex layouts, and tables.
- OCR is not currently implemented.
- Citation validation is based on expected-page and expected-fact checks rather than an independent claim verification system.
- Cross-encoder scores are ranking scores, not calibrated confidence scores.
- Uploaded documents, indexes, and logs are stored in the runtime environment and may not persist after the session ends.

## Setup

1. Install the required dependencies from `requirements.txt`.
2. Provide an OpenAI API key when prompted.
3. Run the notebook in Google Colab.
4. Upload a PDF document through the Gradio interface.
5. Build the index and start asking questions.

The API key is requested through a hidden input and should never be hardcoded or committed to GitHub.

## Security Note

Do not upload API keys, private PDF documents, or sensitive interaction logs to a public repository.

## Project Type

Portfolio project — Hybrid Retrieval-Augmented Generation (RAG) prototype.
