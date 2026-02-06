# AI Research Paper Helper

> 🧠 AI-powered browser extension for understanding research papers faster

A production-ready Chrome extension with Python backend that provides:
- **Smart Article Detection** - Works on arXiv, Medium, and research blogs
- **Multi-level Summarization** - TL;DR, Technical, and Beginner-friendly summaries
- **Equation Explanation** - LaTeX to plain English with variable definitions
- **Key Contribution Extraction** - Datasets, metrics, algorithms, and novel claims
- **RAG-based Q&A** - Ask questions and get cited answers from the paper

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    Chrome Extension (Frontend)                   │
├─────────────────────────────────────────────────────────────────┤
│  Content Script     │  Popup UI    │  Sidebar    │  Background  │
│  - Page detection   │  - Actions   │  - Summary  │  - API calls │
│  - DOM extraction   │  - Settings  │  - Q&A      │  - State     │
│  - Equation hooks   │  - Status    │  - Chips    │  - Routing   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼ HTTP/JSON
┌─────────────────────────────────────────────────────────────────┐
│                    FastAPI Backend (Python)                      │
├─────────────────────────────────────────────────────────────────┤
│  /summarize      │  /explain-equations  │  /extract-key-points  │
│  /rag/index      │  /rag/query          │  /health              │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                       ML Pipeline                                │
├─────────────────────────────────────────────────────────────────┤
│  Embeddings: all-MiniLM-L6-v2    │  Summarization: BART-large   │
│  Vector Store: FAISS (IndexFlatIP) │  Keywords: YAKE + patterns │
│  LLM (optional): OpenRouter/Groq   │  Text: spaCy + regex       │
└─────────────────────────────────────────────────────────────────┘
```

## 🚀 Quick Start

### Backend Setup

```bash
cd backend
pip install -r requirements.txt
python -m spacy download en_core_web_sm  # Optional, for better NLP
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`

### Extension Setup

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable "Developer mode" (toggle in top right)
3. Click "Load unpacked"
4. Select the `extension/` folder
5. The extension icon should appear in your toolbar

### Configuration (Optional)

For enhanced summarization and equation explanation, set API keys:

```bash
# In backend/.env
AIHELPER_OPENROUTER_API_KEY=your_key_here
# or
AIHELPER_GROQ_API_KEY=your_key_here
```

## 📁 Project Structure

```
extension/
├── extension/               # Chrome Extension
│   ├── manifest.json        # Extension config
│   ├── background.js        # Service worker
│   ├── content.js           # Page injection
│   ├── content.css          # Injected styles
│   ├── popup/               # Extension popup
│   └── utils/               # Shared utilities
│
├── backend/                 # FastAPI Backend
│   ├── main.py              # App entry point
│   ├── config.py            # Configuration
│   ├── routers/             # API endpoints
│   ├── services/            # Business logic
│   └── ml/                  # ML pipeline
│
└── docs/                    # Documentation
```

## 🎯 Features

### Page Detection
- **arXiv**: Detects abstract pages and extracts title, abstract, authors, equations
- **Medium**: Extracts article content, author, sections
- **Blogs**: Heuristic detection for article-like pages

### Summarization
| Level | Audience | Output |
|-------|----------|--------|
| TL;DR | Everyone | 5-6 bullet points |
| Technical | ML Researchers | 2-3 paragraphs with terminology |
| Beginner | Non-experts | Plain English explanation |

### Equation Explanation
```
Input:  \mathcal{L} = -\sum_i y_i \log(\hat{y}_i)
Output:
  Readable: L = -Σᵢ yᵢ · log(ŷᵢ)
  Meaning:  Cross-entropy loss measuring prediction error
  Variables: y (true label), ŷ (prediction), i (sample index)
  Importance: Drives model training for classification tasks
```

### RAG Q&A
- Chunks paper with 512 token windows, 64 token overlap
- Embeds with sentence-transformers (384-dim vectors)
- FAISS similarity search for retrieval
- Answers grounded in paper content with citations

## 🔧 API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/summarize` | POST | Multi-level summarization |
| `/explain-equations` | POST | Equation explanation |
| `/extract-key-points` | POST | Key contribution extraction |
| `/rag/index` | POST | Index paper for Q&A |
| `/rag/query` | POST | Ask questions about paper |
| `/rag/status` | GET | Get indexed papers |

See `/docs` for full OpenAPI documentation.

## 🔮 Future Roadmap

- [ ] PDF direct parsing (no HTML required)
- [ ] Cross-paper comparison and analysis
- [ ] Citation graph visualization
- [ ] Offline mode with cached embeddings
- [ ] Export summaries to Notion/Markdown
- [ ] Multi-language support

## 📜 License

MIT License - see LICENSE file for details.
