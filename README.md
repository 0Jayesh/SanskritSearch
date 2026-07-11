# SanskritSearch

A multilingual semantic retrieval system for Bhagavad Gita verses, 
built by fine-tuning an embedding model on Sanskrit-English parallel data.

## What this is

Given a question in English or Hinglish, the system retrieves the most 
relevant Bhagavad Gita verse (Sanskrit + English) and generates a 
grounded answer using an LLM.

## Results

| Stage | Recall@5 |
|---|---|
| Baseline (no fine-tuning) | 2.57% |
| Fine-tuned (3 epochs) | 26.86% |
| Fine-tuned (15 epochs) | 80.71% |

Total failures: 135 / 700. Most failures occur on generic queries 
(e.g. "What did Arjun say?") that match multiple verses semantically.

## Dataset

Bhagavad Gita — 700 Sanskrit verses with English translations  
Source: Henil1/Sans-eng (HuggingFace)

700 synthetic queries generated via Groq (Llama-3.1), one per verse. 
Queries generated in Hinglish to reflect how Indian users naturally search.

## Stack

- SentenceTransformers — embedding model fine-tuning
- paraphrase-multilingual-MiniLM-L12-v2 — base model
- ChromaDB — vector store
- Groq (Llama-3.1-8b) — query generation + RAG answer generation
- Google Colab T4 GPU

## Setup

pip install sentence-transformers chromadb datasets langchain-groq

Load pairs.json and the fine-tuned model, then run the notebook.

## Files

- `pythonCode.ipynb` — full notebook with all steps
- `pairs.json` — 700 generated query-document pairs

## Model

Fine-tuned models available on HuggingFace:  
https://huggingface.co/jayeshkumeriya/sanskrit-gita-retrieval
