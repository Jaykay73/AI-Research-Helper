# Contributing to AI Research Paper Helper

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing to this project.

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- pip or conda for package management

### Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/ai-research-paper-helper.git
   cd ai-research-paper-helper/backend
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

5. **Download spaCy model (optional, for better NLP)**
   ```bash
   python -m spacy download en_core_web_sm
   ```

6. **Run the development server**
   ```bash
   uvicorn main:app --reload
   ```

## 📝 Code Style

### Python Style Guide

- Follow [PEP 8](https://peps.python.org/pep-0008/) conventions
- Use type hints for function parameters and return values
- Write docstrings for all public functions and classes
- Keep lines under 100 characters

### Example

```python
async def process_text(
    content: str,
    max_length: int = 512
) -> dict[str, str]:
    """
    Process text content for analysis.
    
    Args:
        content: The text content to process
        max_length: Maximum token length (default: 512)
    
    Returns:
        Dictionary containing processed results
    
    Raises:
        ValueError: If content is empty
    """
    if not content:
        raise ValueError("Content cannot be empty")
    # Implementation...
```

## 🔄 Pull Request Process

1. **Fork the repository** and create your branch from `main`

2. **Make your changes** with clear, descriptive commits

3. **Add tests** for any new functionality

4. **Run tests** to ensure everything passes:
   ```bash
   pytest tests/ -v
   ```

5. **Update documentation** if you've changed APIs or added features

6. **Submit a pull request** with a clear description of:
   - What changes you made
   - Why you made them
   - Any breaking changes

## 🐛 Reporting Bugs

When reporting bugs, please include:

- Python version
- Operating system
- Steps to reproduce
- Expected behavior
- Actual behavior
- Error messages/stack traces

## 💡 Feature Requests

Feature requests are welcome! Please describe:

- The problem you're trying to solve
- Your proposed solution
- Alternative solutions you've considered

## 📁 Project Structure

```
backend/
├── main.py              # FastAPI app entry point
├── config.py            # Configuration management
├── routers/             # API endpoint handlers
│   ├── summarize.py     # Summarization endpoints
│   ├── equations.py     # Equation explanation
│   ├── keypoints.py     # Key point extraction
│   └── rag.py           # RAG Q&A endpoints
├── services/            # Business logic
│   ├── summarizer.py    # Summarization service
│   ├── equation_explainer.py
│   ├── keyword_extractor.py
│   └── rag_engine.py    # RAG implementation
├── ml/                  # ML pipeline
│   ├── models.py        # Model management
│   ├── embeddings.py    # Embedding utilities
│   └── text_processor.py
└── tests/               # Test suite
```

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.
