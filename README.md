# Custom Research Bot Using LLMs and RAG

This project implements a **Custom Research Bot** using Large Language Models (LLMs) and **Retrieval-Augmented Generation (RAG)** to process documents (PDFs) and provide insightful answers to user queries. The bot integrates various tools such as OpenAI's GPT models, Langchain, and FAISS for effective document retrieval and processing.

## Features
- **Natural Language Queries**: Ask the bot questions about PDF documents, and it will return relevant and concise answers.
- **PDF Parsing**: Automatically loads and splits PDF documents into smaller, coherent chunks to retain context.
- **Vector Similarity Search**: Uses FAISS to perform fast and accurate similarity searches across document vectors.
- **Conversational Retrieval**: Supports follow-up questions with context awareness using a Conversational Retrieval Chain.

## Technology Stack
- **OpenAI API**: LLM for generating human-like responses.
- **Langchain**: Handles document parsing, text splitting, and integration with vector stores.
- **FAISS**: Facebook AI Similarity Search for vector-based document retrieval.
- **PyPDF**: To read and process PDF files.
- **Python**: Core programming language used in the project.
- **Colab**: Google Colab for running and testing the project.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/research-bot-llm-rag.git
   cd research-bot-llm-rag
   ```

2. Install the required dependencies:
   ```bash
   pip install openai langchain langchain_community faiss-cpu pypdf tiktoken
   ```

## How to Use

1. **Set OpenAI API Key**:  
   Add your OpenAI API key:
   ```python
   OPENAI_API_KEY = "your-api-key"
   ```

2. **Load and Process PDF**:  
   Use the PyPDFLoader to load your PDF document:
   ```python
   from langchain.document_loaders import PyPDFLoader
   pdf_reader = PyPDFLoader("/path/to/your/document.pdf")
   documents = pdf_reader.load()
   ```

3. **Split Text into Chunks**:  
   Use `RecursiveCharacterTextSplitter` to split the document for better processing:
   ```python
   text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
   chunks = text_splitter.split_documents(documents)
   ```

4. **Create Embeddings and Vector Store**:  
   Generate embeddings and create a FAISS vector store for fast retrieval:
   ```python
   from langchain.vectorstores import FAISS
   from langchain.embeddings import OpenAIEmbeddings
   embeddings = OpenAIEmbeddings(api_key=OPENAI_API_KEY)
   db = FAISS.from_documents(documents=chunks, embedding=embeddings)
   ```

5. **Ask a Query**:  
   Use the `ConversationalRetrievalChain` to ask questions about the document:
   ```python
   from langchain.chains import ConversationalRetrievalChain
   query = "What is this document about, explain in just 3-4 lines"
   result = qa({"question": query, "chat_history": []})
   print(result["answer"])
   ```

## Example Output

```text
Q: What is this document about, explain in just 3-4 lines?
A: This document provides an overview of Artificial Intelligence, Machine Learning, and Deep Learning concepts, detailing their applications and advancements in cognitive research.
```

## Future Enhancements
- **UI Integration**: Build a simple web-based UI using Streamlit for interactive querying.
- **Support for Multiple Document Formats**: Extend support to other formats like Word, plain text, etc.
- **Improved Conversational Abilities**: Incorporate memory mechanisms for better follow-up questions.

## Contributing
Contributions are welcome! Please submit a pull request or open an issue to discuss changes.
