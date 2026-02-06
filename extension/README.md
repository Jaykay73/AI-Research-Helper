# AI Research Paper Helper - Chrome Extension

A Chrome extension that provides AI-powered tools for understanding research papers.

## ✨ Features

- **📝 Smart Summarization** - Get TL;DR, technical, and beginner-friendly summaries
- **🔢 Equation Explanation** - Hover over LaTeX equations for plain English explanations
- **💡 Key Point Extraction** - Identify main contributions, datasets, and metrics
- **💬 RAG-based Q&A** - Ask questions and get cited answers from the paper
- **📊 Interactive Sidebar** - All features in a non-intrusive sidebar UI

## 🚀 Installation

### From Source (Developer Mode)

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/ai-research-paper-helper.git
   ```

2. Open Chrome and navigate to `chrome://extensions/`

3. Enable **Developer mode** (toggle in top right)

4. Click **Load unpacked**

5. Select the `extension/` folder

6. The extension icon should appear in your toolbar

## 📖 Usage

### Supported Sites
- **arXiv** - Research paper abstracts and full papers
- **Medium** - Technical articles
- **Research blogs** - Auto-detected article pages

### Quick Actions

1. **Click the extension icon** to open the popup
2. Use the **Quick Actions** buttons:
   - 📝 **Summarize** - Generate multi-level summaries
   - 🔢 **Equations** - Highlight and explain equations
   - 💡 **Key Points** - Extract main contributions
   - 📊 **Open Sidebar** - Full-featured sidebar

### RAG Q&A

1. Navigate to a research paper
2. Click **Summarize** or **Open Sidebar** to index the paper
3. Ask questions in the Q&A section
4. Get answers with citations from the paper

## ⚙️ Settings

Access settings via the gear icon in the popup:

| Setting | Description |
|---------|-------------|
| **API Mode** | Hybrid (recommended), Local only, or API only |
| **Backend URL** | URL of the backend API server |
| **Auto-analyze** | Automatically analyze papers on page load |

## 🏗️ Project Structure

```
extension/
├── manifest.json       # Extension configuration (MV3)
├── background.js       # Service worker for API calls
├── content.js          # Page injection and UI
├── content.css         # Injected styles
├── popup/              # Extension popup UI
│   ├── popup.html
│   ├── popup.css
│   └── popup.js
├── utils/              # Shared utilities
│   ├── api.js          # API communication
│   ├── extractors.js   # Content extraction
│   └── latex-parser.js # LaTeX to readable text
└── icons/              # Extension icons
```

## 🔧 Development

### Prerequisites
- Chrome browser
- Backend server running (see `backend/README.md`)

### Making Changes

1. Edit source files
2. Go to `chrome://extensions/`
3. Click the refresh icon on the extension card
4. Reload the page you're testing on

### Debugging

- **Popup**: Right-click extension icon → Inspect popup
- **Content Script**: Open page DevTools → Console
- **Background**: Extensions page → Inspect views: service worker

## 🔒 Permissions

| Permission | Purpose |
|------------|---------|
| `activeTab` | Access current tab content |
| `storage` | Save user settings |
| `scripting` | Inject content scripts |
| `host_permissions` | Access arxiv.org, medium.com, and other sites |

## 📄 License

MIT License - See [LICENSE](../backend/LICENSE) for details.
