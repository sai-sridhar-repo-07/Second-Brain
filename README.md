# 🧠 Second Brain — AI-Powered Knowledge Base

A personal knowledge base system where AI acts as your librarian. Drop any article, paper, or notes into the `raw/` folder — the AI reads it, extracts concepts, people, and ideas, cross-links everything, and builds a searchable wiki automatically.

Built on the [Karpathy Second Brain pattern](https://karpathy.ai) using Claude Code + Obsidian.

---

## 📸 What It Looks Like

> Drop a paper → AI ingests it → Obsidian shows a connected knowledge graph

Currently contains **21 sources**, **29 researcher profiles**, **18 concept pages** — all auto-generated and cross-linked.

---

## 📁 Folder Structure

```
second-brain/
  raw/              ← Drop your sources here (never edited by AI)
  wiki/
    sources/        ← One summary page per ingested source
    entities/       ← People, companies, tools
    concepts/       ← Ideas, frameworks, theories
    synthesis/      ← Cross-topic analyses and answers
    index.md        ← Master catalog of all pages
    log.md          ← Full history of every operation
  outputs/          ← Saved query results and reports
  CLAUDE.md         ← The AI's instructions (schema + rules)
  README.md         ← This file
```

---

## ⚡ Quick Start

### 1. Clone the repo

```bash
git clone https://github.com/sai-sridhar-repo-07/Second-Brain.git
cd Second-Brain
```

### 2. Open in Obsidian

1. Open **Obsidian** → click **"Open folder as vault"**
2. Select the cloned `Second-Brain` folder
3. Your wiki is live — browse the graph view to see all connections

### 3. Pick your AI (see options below)

---

## 🤖 AI Options — Free and Paid

You can run this second brain with **Claude (paid)** or **free LLMs**. Here's how to set up each.

---

### Option 1 — Claude Code (Recommended, Paid)

The system was built and tested with Claude Code. Best quality, understands the CLAUDE.md schema natively.

**Cost**: ~$0.01–0.05 per ingestion depending on source length. Very cheap for occasional use.

#### Setup

1. Get an API key from [console.anthropic.com](https://console.anthropic.com)
2. Install Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

3. Set your API key:

```bash
export ANTHROPIC_API_KEY=your_key_here
```

4. Open this folder in Claude Code:

```bash
cd Second-Brain
claude
```

5. Ingest a source:

```
I added raw/my-article.md — please ingest it into the wiki
```

---

### Option 2 — Groq (Free, Fast)

Groq offers a **free tier** with fast inference on open-source models (LLaMA 3, Mixtral). Best free option.

**Cost**: Free tier includes ~14,400 tokens/minute on LLaMA 3 70B

#### Setup

1. Sign up at [console.groq.com](https://console.groq.com) — no credit card required
2. Create a free API key
3. Install the Groq Python SDK:

```bash
pip install groq
```

4. Create a file `ingest.py` in your Second Brain folder:

```python
import os
from groq import Groq

client = Groq(api_key=os.environ.get("GROQ_API_KEY"))

def read_file(path):
    with open(path, "r") as f:
        return f.read()

def write_file(path, content):
    os.makedirs(os.path.dirname(path), exist_ok=True)
    with open(path, "w") as f:
        f.write(content)

def ingest_source(raw_file_path):
    schema = read_file("CLAUDE.md")
    source = read_file(raw_file_path)
    source_name = os.path.basename(raw_file_path).replace(".md", "")

    prompt = f"""
You are a knowledge base librarian. Here is your schema:

{schema}

Here is a new source to ingest from raw/{source_name}.md:

{source}

Please create:
1. A wiki/sources/{source_name}.md summary page
2. Any new concept pages needed in wiki/concepts/
3. Any new entity pages needed in wiki/entities/

Return each file as:
FILE: wiki/sources/{source_name}.md
[content]
---
FILE: wiki/concepts/concept-name.md
[content]
---
"""

    response = client.chat.completions.create(
        model="llama-3.3-70b-versatile",  # free tier model
        messages=[{"role": "user", "content": prompt}],
        max_tokens=4000,
    )

    result = response.choices[0].message.content
    # Parse and write files
    for block in result.split("---"):
        if block.strip().startswith("FILE:"):
            lines = block.strip().split("\n")
            file_path = lines[0].replace("FILE:", "").strip()
            content = "\n".join(lines[1:]).strip()
            write_file(file_path, content)
            print(f"Created: {file_path}")

# Usage:
# python ingest.py raw/my-article.md
if __name__ == "__main__":
    import sys
    if len(sys.argv) > 1:
        ingest_source(sys.argv[1])
    else:
        print("Usage: python ingest.py raw/your-file.md")
```

5. Set your key and run:

```bash
export GROQ_API_KEY=your_groq_key_here
python ingest.py raw/my-article.md
```

**Available free models on Groq:**

| Model | Context | Best For |
|-------|---------|----------|
| `llama-3.3-70b-versatile` | 128k | Best quality free option |
| `llama-3.1-8b-instant` | 128k | Fastest, basic ingestion |
| `mixtral-8x7b-32768` | 32k | Good reasoning |

---

### Option 3 — Google Gemini (Free Tier)

Google's Gemini API has a **generous free tier** (15 requests/minute, 1M tokens/day on Gemini 1.5 Flash).

**Cost**: Free tier is very generous for personal use

#### Setup

1. Get a free API key at [aistudio.google.com](https://aistudio.google.com) — sign in with Google
2. Install the SDK:

```bash
pip install google-generativeai
```

3. Create `ingest_gemini.py`:

```python
import os
import google.generativeai as genai

genai.configure(api_key=os.environ.get("GEMINI_API_KEY"))
model = genai.GenerativeModel("gemini-1.5-flash")  # free tier

def read_file(path):
    with open(path, "r") as f:
        return f.read()

def write_file(path, content):
    os.makedirs(os.path.dirname(path), exist_ok=True)
    with open(path, "w") as f:
        f.write(content)

def ingest_source(raw_file_path):
    schema = read_file("CLAUDE.md")
    source = read_file(raw_file_path)
    source_name = os.path.basename(raw_file_path).replace(".md", "")

    prompt = f"""
You are a knowledge base librarian. Here is your schema:

{schema}

Ingest this source (raw/{source_name}.md):

{source}

Create wiki pages in this format:
FILE: wiki/sources/{source_name}.md
[content]
---
FILE: wiki/concepts/concept-name.md
[content]
---
"""

    response = model.generate_content(prompt)
    result = response.text

    for block in result.split("---"):
        if block.strip().startswith("FILE:"):
            lines = block.strip().split("\n")
            file_path = lines[0].replace("FILE:", "").strip()
            content = "\n".join(lines[1:]).strip()
            write_file(file_path, content)
            print(f"Created: {file_path}")

if __name__ == "__main__":
    import sys
    if len(sys.argv) > 1:
        ingest_source(sys.argv[1])
    else:
        print("Usage: python ingest_gemini.py raw/your-file.md")
```

4. Run:

```bash
export GEMINI_API_KEY=your_gemini_key_here
python ingest_gemini.py raw/my-article.md
```

**Available free Gemini models:**

| Model | Context | Notes |
|-------|---------|-------|
| `gemini-1.5-flash` | 1M tokens | Best free option — fast and capable |
| `gemini-1.5-flash-8b` | 1M tokens | Faster, smaller |

---

### Option 4 — Ollama (100% Free, Runs Locally)

Run LLMs entirely on your own machine — no API key, no internet, no cost.

**Cost**: Completely free. Requires a decent machine (8GB+ RAM for smaller models, 16GB+ for 7B+)

#### Setup

1. Install Ollama from [ollama.com](https://ollama.com)

2. Pull a model:

```bash
ollama pull llama3.2        # 3B — fast, works on most machines
ollama pull llama3.1:8b     # 8B — better quality
ollama pull mistral         # 7B — good for reasoning
```

3. Install Python client:

```bash
pip install ollama
```

4. Create `ingest_ollama.py`:

```python
import os
import ollama

def read_file(path):
    with open(path, "r") as f:
        return f.read()

def write_file(path, content):
    os.makedirs(os.path.dirname(path), exist_ok=True)
    with open(path, "w") as f:
        f.write(content)

def ingest_source(raw_file_path, model="llama3.2"):
    schema = read_file("CLAUDE.md")
    source = read_file(raw_file_path)
    source_name = os.path.basename(raw_file_path).replace(".md", "")

    prompt = f"""
You are a knowledge base librarian. Schema:

{schema}

Ingest this source (raw/{source_name}.md):

{source}

Return wiki pages in this format only:
FILE: wiki/sources/{source_name}.md
[content]
---
FILE: wiki/concepts/concept-name.md
[content]
---
"""

    response = ollama.chat(
        model=model,
        messages=[{"role": "user", "content": prompt}]
    )

    result = response["message"]["content"]

    for block in result.split("---"):
        if block.strip().startswith("FILE:"):
            lines = block.strip().split("\n")
            file_path = lines[0].replace("FILE:", "").strip()
            content = "\n".join(lines[1:]).strip()
            write_file(file_path, content)
            print(f"Created: {file_path}")

if __name__ == "__main__":
    import sys
    model = sys.argv[2] if len(sys.argv) > 2 else "llama3.2"
    if len(sys.argv) > 1:
        ingest_source(sys.argv[1], model)
    else:
        print("Usage: python ingest_ollama.py raw/your-file.md [model]")
        print("Example: python ingest_ollama.py raw/bert.md mistral")
```

5. Run (no API key needed):

```bash
python ingest_ollama.py raw/my-article.md
# or specify model:
python ingest_ollama.py raw/my-article.md mistral
```

---

## 📊 Comparison: Which AI Should I Use?

| Option | Cost | Quality | Speed | Setup |
|--------|------|---------|-------|-------|
| Claude Code | ~$0.01–0.05/source | ⭐⭐⭐⭐⭐ | Fast | Easy |
| Groq (LLaMA 3 70B) | Free | ⭐⭐⭐⭐ | Very fast | Easy |
| Gemini 1.5 Flash | Free | ⭐⭐⭐⭐ | Fast | Easy |
| Ollama (local) | Free | ⭐⭐⭐ (depends on model) | Slow on CPU | Medium |

**Recommendation:**
- **Just getting started?** → Use Groq (free, fast, great quality)
- **Best results?** → Use Claude Code
- **Privacy / offline?** → Use Ollama
- **Google user?** → Use Gemini

---

## 🔄 Basic Workflow (Any AI Option)

```
1. Find something interesting (article, paper, notes)
2. Save as a .md file in raw/
3. Run the ingestion command
4. Open Obsidian to browse the updated wiki
5. Ask the AI questions about your knowledge base
```

### Adding a Source

```bash
# Save your content
echo "# My Article\n[paste content]" > raw/my-article.md

# Ingest with your chosen AI
python ingest.py raw/my-article.md          # Groq
python ingest_gemini.py raw/my-article.md   # Gemini
python ingest_ollama.py raw/my-article.md   # Ollama
# OR open Claude Code in this folder and say "ingest raw/my-article.md"
```

### Asking Questions

With Claude Code (best experience):
```
Open Claude Code in this folder and ask anything:
"What is RAG and how does it differ from fine-tuning?"
"Who founded Anthropic and what papers did they write first?"
"Compare all normalization techniques in the wiki"
```

With free LLMs, modify the ingestion scripts to take a `--query` flag instead of `--ingest`.

---

## 📚 What's Already In This Wiki

This repo ships with **21 pre-ingested foundational AI papers**:

**Foundational Architectures**
- Attention Is All You Need (Transformer, 2017)
- BERT (2018) · GPT-3 (2020) · ResNet (2015) · AlexNet (2012) · Diffusion Models (2020)

**Training Techniques**
- Adam Optimizer (2014) · Batch Normalization (2015) · Dropout (2014) · Layer Normalization (2016)

**Modern LLM Techniques**
- LoRA (2021) · Constitutional AI (2022) · Chain-of-Thought (2022) · RAG (2020)

**Emerging Paradigms + Bonus**
- Mixture of Experts (2022) · FlashAttention (2022) · Word2Vec (2013) · GANs (2014) · AlphaGo/Zero (2016–2018) · Vision Transformer (2020) · Scaling Laws (2020)

---

## 🛠 Requirements

- **Obsidian** (free) — [obsidian.md](https://obsidian.md)
- **Python 3.8+** — for free LLM scripts
- **Claude Code** (optional) — for best experience

---

## 📄 License

MIT — use this freely for personal or commercial projects.

---

## ⭐ If This Helped You

Star the repo and share what you build with it.
Tag `#SecondBrain #AI #PKM` on Instagram/Twitter.
