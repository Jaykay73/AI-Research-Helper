# Setup & Deployment Guide

## Prerequisites

- **Python 3.9+** - Required for the backend
- **Node.js 16+** - Optional, for extension development
- **Chrome/Chromium** - For running the extension
- **~2GB RAM** - For loading ML models (more if using GPU)

## Backend Installation

### 1. Create Virtual Environment

```bash
cd backend
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt

# Optional: Better NLP support
python -m spacy download en_core_web_sm
```

### 3. Configure Environment

Create a `.env` file in the `backend/` directory:

```env
# API Mode: 'local', 'api', or 'hybrid'
AIHELPER_API_MODE=hybrid

# Optional: LLM API keys for enhanced features
AIHELPER_OPENROUTER_API_KEY=your_openrouter_key
AIHELPER_GROQ_API_KEY=your_groq_key

# Server settings (defaults shown)
AIHELPER_HOST=0.0.0.0
AIHELPER_PORT=8000
AIHELPER_DEBUG=true
```

### 4. Start the Server

```bash
# Development (with auto-reload)
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Production
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

Verify the server is running: `http://localhost:8000/health`

## Extension Installation

### Development Mode

1. Open Chrome and go to `chrome://extensions/`
2. Enable **Developer mode** (toggle in top right)
3. Click **Load unpacked**
4. Navigate to and select the `extension/` folder
5. The AI Research Helper icon should appear in your toolbar

### Production Build

For distribution, you would:
1. Create icons in all required sizes (16, 48, 128 px)
2. Package with `chrome.developerPrivate.packDirectory` or `zip`
3. Submit to Chrome Web Store

## GPU Acceleration (Optional)

For faster inference with CUDA:

```bash
# Uninstall CPU-only torch
pip uninstall torch

# Install CUDA-enabled torch (check your CUDA version)
pip install torch --index-url https://download.pytorch.org/whl/cu118
```

## Docker Deployment

Create a `Dockerfile` in `backend/`:

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Build and run:

```bash
docker build -t ai-research-helper .
docker run -p 8000:8000 -e AIHELPER_API_MODE=hybrid ai-research-helper
```

## Troubleshooting

### "Backend not available" in extension
- Ensure the backend is running on `http://localhost:8000`
- Check CORS settings in `main.py` allow your origin

### "Paper not indexed" error
- Click "Analyze Paper" first before asking questions
- Check backend logs for indexing errors

### Slow first request
- First request loads ML models (~5-10 seconds)
- Subsequent requests are much faster

### Out of memory
- Reduce `chunk_size` in `config.py`
- Use API mode instead of local models

## Health Checks

| Endpoint | Expected Response |
|----------|-------------------|
| `GET /health` | `{"status": "healthy", ...}` |
| `GET /` | API info with endpoints |
| `GET /docs` | Swagger UI |
