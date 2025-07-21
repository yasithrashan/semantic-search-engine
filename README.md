# Semantic Search Engine

A Python-based semantic search engine that processes PDF documents and enables natural language queries using Google's Generative AI embeddings. This project demonstrates how to build a document retrieval system that understands the meaning behind queries, not just keyword matches.

## Features

- **PDF Document Processing**: Load and parse PDF documents using PyPDF
- **Intelligent Text Chunking**: Split documents into manageable chunks with overlap for context preservation
- **Semantic Embeddings**: Generate vector embeddings using Google's Gemini AI models
- **Similarity Search**: Find relevant document sections based on semantic similarity
- **Score-based Results**: Get similarity scores to evaluate result relevance

## Prerequisites

- Google Colab account
- Google Gemini API key
- LangSmith API key (optional, for tracing)

## Setup

### 1. Get Your API Keys

- **Gemini API Key**: Get from [Google AI Studio](https://makersuite.google.com/app/apikey)
- **LangSmith API Key**: (Optional) Get from [LangSmith](https://smith.langchain.com/)

### 2. Store API Keys in Colab Secrets

1. Click the key icon (🔑) in the left sidebar of your Colab notebook
2. Add `geminiapikey` with your Gemini API key
3. Add `LANGSMITH_API_KEY` with your LangSmith key (optional)

### 3. Upload Your PDF

Upload your PDF document to the Colab environment using the file upload feature or by mounting Google Drive.

## Quick Start in Google Colab

1. **Open the notebook** in Google Colab
2. **Set up API keys** in Colab secrets (🔑 icon)
3. **Upload your PDF** to the `/content/` directory
4. **Run all cells** - the notebook will:
   - Install required packages automatically
   - Load and process your PDF
   - Create embeddings and vector store
   - Enable semantic search queries

### Basic Usage

```python
# The notebook handles setup automatically
# Just modify the file path to your PDF
file_path = '/content/your-document.pdf'

# Then use the search functionality
results = vector_store.similarity_search("Your question here")
print(results[0].page_content)
```

### Advanced Search with Scores

```python
# Get results with similarity scores
results = vector_store.similarity_search_with_score("Your query here")
doc, score = results[0]
print(f"Similarity Score: {score}")
print(f"Content: {doc.page_content}")
```

## Configuration Options

### Text Splitting Parameters

- `chunk_size`: Maximum size of each text chunk (default: 1000)
- `chunk_overlap`: Number of characters to overlap between chunks (default: 200)
- `add_start_index`: Whether to add starting character index to metadata (default: True)

### Embedding Model

The project uses Google's `models/embedding-001` which provides:
- High-quality semantic understanding
- Support for multiple languages
- Optimized for search and retrieval tasks

## Example Queries

The system can handle natural language queries such as:

- "How many distribution centers does Nike have in the US?"
- "What was Nike's revenue in 2023?"
- "Tell me about the company's sustainability initiatives"
- "What are the main risk factors mentioned?"

## Project Structure

```
semantic-search-engine/
│
├── Semantic_search_engine.ipynb    # Main Jupyter notebook (run in Colab)
├── README.md                       # This file
└── sample-documents/               # Upload your PDFs here
    └── nke-10k-2023.pdf           # Example Nike 10-K document
```

## Using with Google Drive (Optional)

To access files from Google Drive in Colab:

```python
from google.colab import drive
drive.mount('/content/drive')

# Then reference your PDF like:
file_path = '/content/drive/MyDrive/documents/your-file.pdf'
```

## How It Works

1. **Document Loading**: PDF documents are loaded and parsed into text
2. **Text Chunking**: Large documents are split into smaller, overlapping chunks
3. **Embedding Generation**: Each chunk is converted into a vector embedding using Google's AI
4. **Vector Storage**: Embeddings are stored in an in-memory vector database
5. **Semantic Search**: User queries are embedded and matched against stored vectors
6. **Result Ranking**: Results are returned ranked by semantic similarity

## Limitations

- **Memory Usage**: The InMemoryVectorStore loads all embeddings into RAM
- **PDF Quality**: Results depend on the quality of text extraction from PDFs
- **API Costs**: Google Gemini API calls incur costs based on usage
- **Language Support**: Optimized for English text

## Troubleshooting

### Common Colab Issues

1. **API Key Errors**: Double-check your key is stored correctly in Colab secrets
2. **File Not Found**: Ensure your PDF is uploaded to `/content/` or the correct path
3. **Package Installation**: If packages fail to install, restart runtime and try again
4. **Memory Issues**: For very large PDFs, consider using smaller chunk sizes

### Performance Tips for Colab

- Upload smaller PDF files (under 50MB) for better performance
- Restart runtime if you encounter memory issues
- Use the free GPU runtime for faster embedding generation

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [LangChain](https://langchain.com/) for the document processing framework
- [Google Gemini](https://deepmind.google/technologies/gemini/) for the embedding models
- [PyPDF](https://github.com/py-pdf/PyPDF2) for PDF processing capabilities
