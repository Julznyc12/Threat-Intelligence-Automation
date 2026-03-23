# Threat-Intelligence-Automation
# Week 4 Model Comparison — Threat Intelligence Feed Dashboard

## Overview
This project evaluates multiple machine learning and LLM-based models for classifying and enriching threat intelligence data. The goal is to determine the most effective approach for relevance scoring within a Threat Intelligence Feed Dashboard.

## Models Tested
- Sentiment Analysis (DistilBERT)
- Zero-Shot Classification (BART MNLI)
- Named Entity Recognition (BERT NER)
- LLM Classification (Groq Llama 3)

## Key Findings
- Sentiment analysis was not effective for cybersecurity data
- Zero-shot classification provided strong structured categorization
- Groq LLM produced the most context-aware and accurate severity classifications
- NER was useful for extracting entities but not for classification

## Results Summary
See `results/comparison-table.csv` for full results.

## Files
- `workflow.json` — n8n automation pipeline
- `report.md` — detailed model comparison analysis
- `results/comparison-table.csv` — output data

## Author
Julian Silva-Erazo
