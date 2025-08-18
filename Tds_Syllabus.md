# 📑 Course Roadmap


## 🗂️ Index

> 📌 **Quick Navigation**

- **Week 1 → Development Tools**  

- **Week 2 → Deployment Tools**  

- **Week 3 → LLM APIs**  


- **🚀 Project 1 → ?**  

- **Week 4 → LangChain**  

- **Week 5 → LangGraph**  


- **Week 6 → Quarto Websites & AWK**  

- **🚀 Project 2 → ?**  

- **Week 7 → ?**



> 📌 **Small Projects**  
W1-> **Simple ChatBot (No Memory)**  
W2-> **Memory-Based ChatBot**  
W3-> **PDF ChatBot**  
W4-> **YouTube Playlist QA Assistant**  
W5-> **SQL Query Agent**  
W6-> **Portfolio Website**  
*Voice-enabled AI Chat Assistant*     

---

## Week 1 → Development Tools 🛠

1. **Intro to Linux** (Dual Boot, WSL)  
2. **Language Setup & Config** (`bashrc`, `venv`, `nvm`, etc.)
    - JS → `nvm`, `node`, `npm`, `pnpm`, `yarn`  
    - C/C++ → `gcc` vs `g++`  
    - Java → `jdk`, `jre`, `jvm`  
    - Python → `venv`, `pipx`, `conda`, `uv`  
3. **Git Basics**  
    - `init`, `add`, `commit`, `push`  
    - Undo/redo commits  
4. **FastAPI Basics**  
5. **Ollama Setup**  

>Small Project → **Simple ChatBot (No Memory)**    
    - Build a FastAPI endpoint `/ask` with Ollama (Gemma).  
    - Answers queries **without history**.  

---

## Week 2 → Deployment Tools ☁️

1. **Advanced Git/GitHub**  
    - Branching, Merging, Actions
2. **Docker/Podman**  
    - Dockerfile, Volumes, Networks
3. **Advanced FastAPI**  
4. **Deployment Platforms**  
    - Vercel, Render, GitHub Pages 
5. **EC2 Deployment** with GitHub Actions + Docker  

> Small Project → **Memory-Based ChatBot**  
    - FastAPI endpoint `/chat` with **Gemini LLM**.  
    - Maintains **multi-turn memory** in RAM.  


---

## Week 3 → LLM APIs 🤖

1. **Prompt Engineering**  
    - Zero-shot, Few-shot  
2. **Function Calling**  
3. **Base64 Encoding**  
4. **Vector Databases & RAG**  
5. **OpenAI API Docs** 
6. **PromptFoo**

> Small Project → **PDF ChatBot**  
    - Upload PDF → Extract text → Store in Vector DB.  
    - Build RAG pipeline with **Streamlit UI + FastAPI backend**.  
    - Multi-turn Q&A → returns **answer + page number**.  

---

## 🚀 Project 1 → ?

---

## Week 4 → LangChain ⚡

1. **Pydantic Models**  
2. **Structured Prompts & Output Parsers**  
3. **Chains & Runnables**  
4. **Text Splitters**  
5. **VectorStores in LangChain**  
6. **RAG + Tool Calling**  

> Small Project → *YouTube Playlist QA Assistant*  
    - Scrape **subtitles** from each video of playlist.  
    - Store in a vector DB.  
    - Build chatbot → answers **video-specific queries**.  

---

## Week 5 → LangGraph 🔗

> ⚠️ I Don't have much knowledge on this topic.  

> Small Project → *SQL Query Agent**  
    - Convert **natural language → SQL query**.  
    - Run on DB → Return **tabular results**.  

---

## Week 6 → Quarto Websites & AWK 🌐

1. **Quarto + GitHub Pages**  
2. **RevealJS Presentations**  
3. **Markdown → Website conversion**  
4. **Excel Toolpack** (Correlation, Regression, Data Analysis)  
5. **AWK Basics** (text processing)  

> Small Project → **Portfolio Website**  
    - Publish your portfolio with **Quarto + GitHub Pages**.  

---

## 🚀 Project 2 → ?

## Week 7 → ?

---

## ✨ Bonus Project (Optional)

> Voice-enabled AI Chat Assistant
    - 🎤 Integrate **STT + TTS + LLM**.  
    - Speak → Listen → Respond in real-time.  
