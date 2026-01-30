**Website-Based RAG Chatbot — AI/ML Engineer Assignment
🔍 Project Overview**

This project is a website-based AI chatbot built using a Retrieval-Augmented Generation (RAG) approach. The chatbot takes a website URL as input, crawls and extracts meaningful text from the page, converts it into embeddings, stores them in a vector database, and then answers user questions strictly based on the website content.

The main goal of this project is to make sure the chatbot only answers using the provided website data and does not use outside knowledge. If the answer is not found in the website content, it returns a fixed fallback response:

**“The answer is not available on the provided website.”**

The system also handles spelling mistakes in user questions and still tries to retrieve the correct information from the website.

The project follows a modular RAG pipeline. The flow is:
1 User enters a website URL
2 URL is validated and checked for reachability
3 HTML is fetched from the website
4 Boilerplate content is removed (headers, footers, nav, scripts, ads)
5 Clean text blocks are extracted
6 Text is split into semantic chunks with overlap
7 Embeddings are created for each chunk
8 Embeddings are stored in a persistent vector database
9 User asks a question
10 Question is normalized and spelling is corrected (fuzzy matching)
11 Question embedding is generated
12 Top-k similar chunks are retrieved from vector DB
13 Chunks are reranked and best definition sentences are selected
14 LLM generates an answer using only retrieved context
15 Final answer is cleaned and returned

Framwork Used
**LangChain**
LangChain is used to structure the LLM interaction and document handling in the RAG pipeline. It helps in organizing the retrieval + prompt + answer generation flow.
**LangGraph**
LangGraph is not used in this project because the pipeline is linear and does not require graph-based orchestration.

**LLM Model Used and Why**
**Model Used:** Google Gemini (via LangChain integration)
**Temperature:** 0.0
I chose this model because:
1 It follows instructions well
2 Works reliably with context-grounded prompts
3 Produces stable answers at low temperature
4 Interates easily with LangChain
5 Good quality for question-answering tasks

**Vector Database:** ChromaDB (Persistent)

**Embedding Strategy**

**Embedding Model:** SentenceTransformers — all-MiniLM-L6-v2
**Why this model:**
Lightweight and fast
Good semantic similarity performance
Works well for paragraph-level retrieval
Runs easily on local machine or Colab

**Process:**
Cleaned text chunks are created
Each chunk is embedded
Embeddings are normalized
Stored with metadata (source URL + title)

**Setup and Run Instructions**
**Step 1 — Install Dependencies**
pip install requests validators beautifulsoup4 readability-lxml
pip install sentence-transformers chromadb
pip install langchain langchain-google-genai
pip install rapidfuzz nltk tldextract

**Step 2 — Set API Key**
export GOOGLE_API_KEY=YOUR_KEY

**Step 3 — Run the Program**
Run the file locally on Jupyter or Google collab.

**Step 4 — Usage**
1 Enter a valid website URL
2 Wait for crawling + embedding
3 Ask questions in natural language
4 Type exit to stop

In this project, I built a website-based chatbot using a RAG (Retrieval Augmented Generation) approach. The system takes a URL, extracts useful text from the page, converts it into embeddings, and then answers questions based only on that content. I focused on making sure the answers stay grounded to the website and that the chatbot returns a fixed message when the information is not available.

While building this, I learned how crawling, text cleaning, chunking, embeddings, vector databases, and LLMs work together in a practical pipeline. I also added features like spelling-tolerant query handling and chunk reranking to improve answer quality. The system works well for most text-based websites, but it is not perfect — sometimes retrieval may miss the best chunk, and answers can depend on how clearly the website content is written.

Overall, this project helped me understand how real-world AI question-answering systems are designed, and how important retrieval quality and prompt control are for reducing hallucinations. With more time, the system could be improved with better reranking models, multi-page crawling, and stronger LLMs.
