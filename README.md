# 📚 Chat With Your Documents | RAG, Embeddings & Vector Databases

An AI-powered document question-answering application built using Retrieval-Augmented Generation (RAG), Python, Google Gemini API, Sentence Transformers, ChromaDB, and Streamlit. The application enables users to upload PDF and TXT documents, retrieve relevant information through semantic search, and generate context-aware answers using a Large Language Model (LLM).

Developed as **Project 4** during my Generative AI internship at **Codomax Digital Solutions**.

## 🚀 Project Overview

Large Language Models can sometimes generate incorrect information or hallucinate when answering questions without sufficient context. Retrieval-Augmented Generation addresses this limitation by retrieving relevant information from external knowledge sources before generating a response.

This project implements a document-based RAG pipeline that extracts text from uploaded files, divides it into smaller chunks, converts those chunks into vector embeddings, stores them in a vector database, and retrieves the most relevant sections for a user's question.

The retrieved context is then passed to Google Gemini, which generates an answer grounded in the available document information.

## 🎯 Project Objectives

- Understand the fundamentals of Retrieval-Augmented Generation.
- Explore LLM hallucinations and context-grounded responses.
- Implement document text extraction and preprocessing.
- Apply text chunking with overlapping sections.
- Generate semantic embeddings using Sentence Transformers.
- Store and retrieve document embeddings using ChromaDB.
- Implement semantic similarity search.
- Integrate retrieved context with Google Gemini API.
- Build an interactive document question-answering interface.
- Practise API key security, error handling, testing, and documentation.

## ✨ Features

### 📄 Document Upload and Processing
- Upload PDF and TXT documents.
- Extract readable text from supported files.
- Preprocess text for downstream processing.
- Display document processing status.

### ✂️ Text Chunking
- Divide long documents into smaller text sections.
- Use overlapping chunks to preserve contextual continuity.
- Prepare document content for embedding generation and retrieval.

### 🔢 Embedding Generation
- Use the Sentence Transformers `all-MiniLM-L6-v2` model.
- Convert text chunks into numerical vector representations.
- Represent semantic meaning to support similarity-based retrieval.

### 🗄️ Vector Database
- Store document chunks and embeddings in ChromaDB.
- Perform semantic similarity searches against user queries.
- Use a persistent local database for vector storage.

### 🔍 Semantic Retrieval
- Convert user questions into embeddings.
- Retrieve up to four relevant document chunks.
- Supply the retrieved text as context for answer generation.

### 🤖 Gemini-Powered Answer Generation
- Integrate Google Gemini API for natural-language responses.
- Generate answers using retrieved document context.
- Instruct the model to acknowledge when the context does not contain the answer.
- Treat instructions within document content as untrusted input.

### 🖥️ Interactive User Interface
- Build a simple interface using Streamlit.
- Upload documents and initiate processing.
- Enter questions through a text input.
- Display generated answers and retrieved context.

### 🔐 Error Handling and Security
- Store API credentials in environment variables.
- Use a `.env` file for local configuration.
- Handle missing API keys and document-processing failures.
- Display errors when retrieval or answer generation fails.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Streamlit | Interactive web interface |
| Google Gemini API | LLM-based answer generation |
| Sentence Transformers | Text embedding generation |
| `all-MiniLM-L6-v2` | Pretrained sentence embedding model |
| ChromaDB | Vector storage and semantic retrieval |
| PyPDF | PDF text extraction |
| python-dotenv | Environment variable management |
| Git | Version control |
| GitHub | Source code hosting and documentation |

## 🧠 Understanding the RAG Workflow

The application follows this pipeline:

**Document Upload → Text Extraction → Text Chunking → Embedding Generation → Vector Database → Semantic Retrieval → Context Construction → Gemini API → Generated Answer**

### 1. Document Ingestion
The user uploads a PDF or TXT file. The application extracts its readable text and prepares it for processing.

### 2. Text Chunking
The extracted text is divided into smaller, overlapping chunks. The current implementation uses a chunk size of approximately 800 characters with a 150-character overlap.

### 3. Embedding Generation
The Sentence Transformers model converts each chunk into a numerical vector representing its semantic content.

### 4. Vector Storage
The generated embeddings and their associated text chunks are stored in a ChromaDB collection.

### 5. Query Embedding
When the user asks a question, the same embedding model converts the question into a vector representation.

### 6. Semantic Search
ChromaDB retrieves the most relevant chunks by comparing the query embedding with the stored document embeddings.

### 7. Context-Augmented Generation
The retrieved chunks are combined into a context prompt and submitted to Google Gemini.

### 8. Answer Generation
Gemini generates a natural-language response based on the supplied context. The application also allows users to inspect the retrieved text sections.

## 🏗️ Project Structure

```text
Chat-With-Your-Documents-RAG/
│
├── app.py                 # Main Streamlit application
├── requirements.txt       # Python dependencies
├── .env                   # Private API configuration
├── .gitignore             # Files excluded from Git
├── README.md              # Project documentation
│
└── chroma_db/             # Local vector database
```

**Note:** The `.env` file and `chroma_db/` directory are excluded from GitHub through `.gitignore`. ChromaDB creates its local database files when the application runs.

## ⚙️ Installation and Setup

### Prerequisites

Make sure you have installed:

- Python 3.10 or a compatible version supported by the selected packages.
- Git.
- Visual Studio Code or another Python editor.
- A Google Gemini API key.
- An internet connection for downloading dependencies, the embedding model, and accessing the Gemini API.

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/Chat-With-Your-Documents-RAG.git
```

Navigate to the project directory:

```bash
cd Chat-With-Your-Documents-RAG
```

Replace `YOUR_USERNAME` with your GitHub username.

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure the Gemini API Key

Create a `.env` file in the root directory.

Add the following configuration:

```env
GEMINI_API_KEY=your_actual_api_key_here
GEMINI_MODEL=gemini-2.5-flash
```

Replace the placeholder with your own API key. If the configured model is unavailable to your account, select a currently supported Gemini model.

Generate and manage your API key through Google AI Studio:

https://aistudio.google.com/

**Security:** Never upload your actual API key to GitHub or share it publicly.

### Step 5: Run the Application

Execute the following command:

```bash
streamlit run app.py
```

Streamlit will display a local URL, usually:

http://localhost:8501

Open the URL in your browser to access the application.

## 📖 How to Use the Application

1. Launch the application using Streamlit.
2. Upload a text-based PDF or TXT document.
3. Click **Process Document** to extract the text, create chunks, generate embeddings, and store them in ChromaDB.
4. Wait for the processing success message.
5. Enter a question related to the uploaded document.
6. Click **Get Answer**.
7. Read the generated response.
8. Expand the retrieved-context section to inspect the source text used for the answer.
9. Ask additional questions about the same document.

For the best results, ask clear questions whose answers are likely to appear in the uploaded document.

## 🧪 Testing and Validation

The application should be tested with different documents and question types.

| Test Case | Expected Behaviour |
|---|---|
| Upload a readable PDF | Text is extracted and processed |
| Upload a TXT file | Text is extracted and processed |
| Upload an empty or unreadable document | A suitable error or empty-content message is displayed |
| Ask a relevant question | Relevant context is retrieved and an answer is generated |
| Ask a question absent from the document | The model is instructed to acknowledge insufficient context |
| Omit the Gemini API key | The application displays a configuration error |
| Use an invalid API key | The API request fails and an error is displayed |
| Inspect retrieved context | Retrieved document sections are visible |

These are expected behaviours to validate during testing, not a claim that every test has already passed.

## 🔐 Security and Limitations

### Security Considerations
- Keep API credentials in environment variables.
- Exclude `.env` and private configuration files from version control.
- Avoid uploading confidential documents to services without appropriate permission.
- Remember that document content is sent to the configured LLM API for answer generation.

### Current Limitations
- Supports PDF and TXT files only.
- Scanned PDFs without an embedded text layer require OCR.
- The application maintains one active document collection at a time. Processing another document replaces the existing collection.
- The basic implementation does not maintain a persistent multi-turn conversation history.
- Retrieved chunks are displayed as context sections, but source page numbers and formal citations are not implemented.
- Answer quality depends on document readability, chunking, retrieval relevance, and the selected language model.
- The model is instructed not to invent information, but prompt instructions cannot guarantee that hallucinations will never occur.
- Gemini API availability, rate limits, and usage charges depend on the account and applicable service terms.

## 🔮 Future Improvements

Potential enhancements include:

- Support for multiple documents and collections.
- Add source citations, document names, and page numbers.
- Introduce OCR for scanned PDFs and image-based documents.
- Add conversational memory for follow-up questions.
- Improve chunking through sentence-aware or token-aware splitting.
- Experiment with alternative embedding models.
- Add reranking to improve retrieval relevance.
- Provide configurable retrieval parameters and chunk sizes.
- Implement document deletion and collection management.
- Add automated unit and integration tests.
- Improve the user interface and deployment configuration.
- Deploy the application to a suitable hosting platform.

## 📚 Key Learning Outcomes

Through this project, I gained practical experience with:

- Retrieval-Augmented Generation architecture.
- LLM hallucinations and context-grounded generation.
- Document parsing and text preprocessing.
- Chunking strategies and overlapping text segments.
- Semantic embeddings and vector representations.
- Vector databases and similarity search.
- Retrieval pipelines and prompt construction.
- Google Gemini API integration.
- Streamlit application development.
- Environment variables and API credential security.
- Exception handling, debugging, and testing.
- Git, GitHub, and technical documentation.

## 🏢 Internship Information

**Organisation:** Codomax Digital Solutions  
**Internship:** Generative AI Internship  
**Project:** Project 4, RAG, Embeddings & Vector Databases  
**Application:** Chat With Your Documents

## 🔗 Project Links

- **GitHub Repository:** [Add your repository link]
- **Live Application:** [Add your deployed application link]
- **LinkedIn Project Post:** [Add your LinkedIn post link]

## 👨‍💻 Author

Developed as part of my hands-on learning journey in Generative AI, focusing on building practical AI applications using LLM APIs, semantic search, embeddings, and vector databases.

🔗 GitHub🚀 : [Add your repository link]

---

⭐ If you find this project useful, consider giving the repository a star!

*This project is intended for educational and demonstration purposes.*