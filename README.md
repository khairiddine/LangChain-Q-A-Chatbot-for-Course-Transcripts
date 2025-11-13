# 📚 LangChain Q&A Chatbot for Course Transcripts

An intelligent Q&A chatbot built with LangChain that answers questions about Tableau course content using Retrieval-Augmented Generation (RAG). The system processes PDF transcripts, creates embeddings, and provides contextual answers with source references.

## 🌟 Features

- **PDF Processing**: Automatically loads and processes course transcript PDFs
- **Smart Text Splitting**: Uses Markdown header-based splitting followed by token-based chunking for optimal context preservation
- **Transcript Improvement**: AI-powered transcript formatting and correction (fixing typos, punctuation, and structure)
- **Vector Search**: Chroma vector database with MMR (Maximal Marginal Relevance) search for diverse, relevant results
- **Contextual Answers**: Retrieval-Augmented Generation (RAG) provides accurate answers with source citations
- **Azure OpenAI Integration**: Leverages GPT-4o for high-quality responses and text-embedding-3-small for embeddings

## 🛠️ Technology Stack

- **LangChain**: Framework for building LLM applications
- **Azure OpenAI**: GPT-4o for chat completions and text-embedding-3-small for embeddings
- **Chroma**: Vector database for semantic search
- **PyPDF**: PDF document loading
- **tiktoken**: Token counting and text splitting
- **Python 3.12+**: Core programming language

## 📋 Prerequisites

- Python 3.12 or higher
- Azure OpenAI account with deployed models:
  - GPT-4o deployment
  - text-embedding-3-small deployment
- Azure OpenAI API key and endpoint

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/langchain-qa-chatbot.git
   cd langchain-qa-chatbot
   ```

2. **Install required packages**
   ```bash
   pip install langchain-community pypdf
   pip install langchain-openai
   pip install tiktoken
   pip install "langchain-chroma>=0.1.2"
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the project root:
   ```env
   AZURE_OPENAI_API_KEY=your_api_key_here
   AZURE_OPENAI_ENDPOINT=your_endpoint_here
   AZURE_OPENAI_API_VERSION=2024-02-15-preview
   AZURE_OPENAI_DEPLOYMENT_NAME=gpt-4o
   AZURE_OPENAI_EMBEDDING_DEPLOYMENT=text-embedding-3-small
   ```

## 📖 Usage

### Running the Notebook

1. Open `LangChain_Project.ipynb` in Jupyter or VS Code
2. Run cells sequentially from top to bottom
3. The notebook will:
   - Load your PDF course transcript
   - Split and process the content
   - Create embeddings and vector store
   - Set up the Q&A chain
   - Answer questions with contextual references

### Example Query

```python
result = chain_retrieving.invoke({
    "question_lecture": "Adding a custom calculation",
    "question_title": "Why are we using SUM here? It's unclear to me.",
    "question_body": "This question refers to calculating the GM%."
})
```

## 🏗️ Project Structure

```
langchain-qa-chatbot/
├── LangChain_Project.ipynb    # Main notebook with complete implementation
├── README.md                   # This file
├── .env                        # Environment variables (create this, not in repo)
├── .gitignore                  # Git ignore file
├── intro-to-tableau/           # Vector store directory (auto-generated)
└── Introduction_to_Tableau.pdf # Your course PDF (add your own)
```

## 🔑 Key Components

### 1. Document Processing Pipeline
- **PDF Loading**: Uses PyPDFLoader to extract text from course transcripts
- **Markdown Splitting**: Splits by headers (#, ##) to preserve lecture structure
- **Transcript Correction**: AI-powered formatting fixes typos and improves readability
- **Token Splitting**: Chunks text into 500-token segments with 50-token overlap

### 2. Vector Store & Retrieval
- **Embeddings**: Azure OpenAI text-embedding-3-small model
- **Vector DB**: Chroma with persistent storage
- **Search Strategy**: MMR (Maximal Marginal Relevance) for diverse results
- **Retrieval**: Returns top 2 most relevant chunks with lambda_mult=0.7

### 3. Q&A Chain
- **Input**: Question with lecture context, title, and body
- **Processing**: Retrieves relevant context from vector store
- **Output**: AI-generated answer with section/lecture citations
- **Model**: Azure OpenAI GPT-4o

## 🔒 Security Notes

⚠️ **IMPORTANT**: Never commit your `.env` file or API keys to GitHub!

- API keys and endpoints are excluded via `.gitignore`
- Always use environment variables for sensitive data
- Rotate keys if accidentally exposed

## 📊 Workflow Overview

```
PDF Document
    ↓
Load & Extract Text (PyPDFLoader)
    ↓
Split by Headers (MarkdownHeaderTextSplitter)
    ↓
AI Transcript Correction (GPT-4o)
    ↓
Token-based Chunking (TokenTextSplitter)
    ↓
Generate Embeddings (text-embedding-3-small)
    ↓
Store in Vector DB (Chroma)
    ↓
User Question → Retrieve Context (MMR Search)
    ↓
Generate Answer (GPT-4o + RAG)
    ↓
Return Answer with Citations
```

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

**Khairiddine**
- GitHub: [@khairiddine](https://github.com/khairiddine)

## 🙏 Acknowledgments

- LangChain for the excellent framework
- Azure OpenAI for powerful language models
- The open-source community

---

**Note**: Replace placeholder values (API keys, GitHub username, PDF filename) with your actual information before using.
