# RAG Security Knowledge Assistant (Flowise + Groq)

## Overview
This project demonstrates a Retrieval-Augmented Generation (RAG) system built using Flowise and Groq. The chatbot answers cybersecurity-related questions using MITRE ATT&CK-based documents as its knowledge source.

## Features
- Document-based question answering
- Source-backed responses (no hallucination)
- Integration with Groq LLM (llama-3.3-70b-versatile)
- Vector-based retrieval using embeddings

## Tech Stack
- Flowise (LLM orchestration)
- Groq (LLM inference)
- HuggingFace (embeddings)
- In-Memory Vector Store

## Knowledge Base
- MITRE ATT&CK – Initial Access
- MITRE ATT&CK – Credential Access
- MITRE ATT&CK – Lateral Movement

## Example Questions
- What is credential dumping?
- How do attackers use phishing for initial access?
- What is lateral movement?

## Chatbot Access
[PASTE YOUR SHARE LINK HERE]

## Screenshots
See the `/screenshots` folder for:
- Chatflow architecture
- Example responses with sources

## Key Takeaway
This project demonstrates how RAG can be used to build a security knowledge assistant that provides accurate, context-aware responses based on trusted documentation.