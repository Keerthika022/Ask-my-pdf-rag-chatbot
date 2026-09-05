
Ask My PDF — RAG Chatbot
A Retrieval-Augmented Generation (RAG) chatbot that answers questions strictly
from uploaded PDF documents, with source and page-number citations. Built as
Project 5 of the AI Internship Projects series.
How it works
PDF(s) → text extraction (pypdf) → chunking (recursive splitter, w/ overlap)
       → embeddings (sentence-transformers: all-MiniLM-L6-v2)
       → vector index (FAISS, cosine similarity)
       → top-k retrieval per question
       → answer generation (Google Gemini API), grounded only in retrieved text
       → inline chat UI (ipywidgets) with citations
      Features
Works with any PDFs — no hardcoded filenames, upload as many as you like
Zero-hallucination guardrail — the model is instructed to answer only
from retrieved passages and say so plainly when the answer isn't there
Per-document filtering — checkboxes in the UI let you scope retrieval
to specific documents
Source citations — every answer lists which document, page, and
similarity score it drew from
Resilient to real API behavior:
retries transient errors (503/500/429-per-minute) with backoff
automatically falls back across multiple Gemini models if one is down
detects free-tier daily quota exhaustion and reports it clearly
instead of retrying forever or misreporting it as an invalid key
dynamically discovers which models your API key can actually call,
instead of trusting a hardcoded model name that may be retired
Secure key handling — the API key is entered via getpass at runtime
and is never hardcoded, logged, or saved to disk
Setup
Option A — Google Colab (recommended)
Open a new Colab notebook.
Upload Glowlogics project 5(ask my pdf).py and run it with: 
%run Glowlogics project 5 (ask my pdf).py
or paste each # %%-marked section into its own cell.
When prompted, upload your PDF(s).
When prompted, paste a free Google AI Studio API key
(get one here).
The last cell renders an inline chat widget — ask away.
Option B — Local Python environment
Bash
(Note: the chat widget requires a Jupyter/Colab environment; running the
.py file directly outside a notebook will use the underlying ask()
function instead of the widget UI.)
Project structure

├── Glowlogics project 5(ask my pdf).py   # full pipeline + UI
├── requirements.txt
├── README.md
└── .gitignore
Notes on API quotas
Google AI Studio's free tier caps requests per day, per model (commonly
20/day on some models). The script surfaces this clearly and automatically
tries other models in its fallback chain rather than failing silently. If
you exhaust the daily quota, wait ~24h, use a different key, or enable
billing in AI Studio.
Tech stack
Python · pypdf · sentence-transformers · FAISS · Google Gemini API ·
ipywidgets
Author
S.Keerthika— AI Internship, Project 5
