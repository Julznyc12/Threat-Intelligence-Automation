# Model Comparison Report — Week 4 
**Name:** Julian Silva-erazo

**Date:** March 20, 2026 

**Capstone Project:** Threat Intelligence Feed Dashboard

**My Component:** Relevance Scorer

## Test Setup 
**Input dataset:** 5 [domain] text samples covering: - 2 clearly concerning/high-severity records - 1 ambiguous/edge case record - 2 routine/benign records 

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment) 
2. facebook/bart-large-mnli (zero-shot classification) 
3. dslim/bert-large-NER (named entity recognition) 
4. Groq Llama 3 8B (LLM classification) 

**Evaluation criteria:** label accuracy, confidence score, speed, ease of 
integration in n8n 

## Results Summary 
The following table compares model outputs across five threat intelligence records:

| Record | Sentiment | Zero-Shot | NER Entities | Groq Severity |
|--------|-----------|-----------|--------------|----------------|
| 1 | NEGATIVE (0.99) | Possible anomaly | IP address | HIGH |
| 2 | NEGATIVE (0.99) | Routine activity | None | INFORMATIONAL |
| 3 | NEGATIVE (0.99) | Possible anomaly | None | MEDIUM |
| 4 | NEGATIVE (0.99) | Possible anomaly | MISC entity | HIGH |
| 5 | NEGATIVE (0.98) | Routine activity | None | INFORMATIONAL |

## Analysis 
**Where models agreed:** 
The zero-shot and Groq models consistently agreed on distinguishing between high-risk and routine events. Records involving suspicious activity (ex: unauthorized login, failed SSH attempts) were identified as anomalous or high severity, while routine events (system updates) were classified as informational or low priority.

**Where models disagreed:** 
The sentimentn model labeled all records as negative, including clear benign events. In contrast, the zero-shot and Groq models provided more context-aware classifications. This is likely due to the sentiment model being training on general language rather than threat intelligence data. 

**Most accurate model overall:** 
The Groq LLM produced the most sensible and context-aware results, it not only classified alerts but also incorporated reasoning, allowing it to better capture the intention and severity of each record. 

**Fastest/most practical:** 
The HuggingFace sentiment model was the fastest and easiest to integrate, but the zero-shot model provided better performance and usefulness. It is more practical for scalable classification tasks due to its structured outputs and relatively low latency.

## Recommended Models for My Capstone Component 
**Component:** Relevance Scoring System  

**Primary model:** 
facebook/bart-large-mnli — Provides structured and reliable classification of alerts into meaningful categories (anomaly vs routine), making it effective for relevance scoring.

**Secondary model (if applicable):** 
Groq — Enhances classification by assigning severity levels and providing contextual reasoning. 

**Rejected models and why:**
distilbert sentiment model: Not suitable for this use case, as it classified nearly all records as negative regardless of actual threat level  

dslim/bert-large-NER: Useful for extracting entities, but not effective as a primary model for determining alert relevance  



## Failure Cases and Limitations 
A key limitation observed was with the sentiment model, which classified all records including clearly benign events such as system updates and backups as negative. This demonstrates that general purpose sentiment models do not apply well to threat intelligence data without domain tuning.  

Additionally, the zero-shot model occasionally produced different classifications depending on how labels were defined, indicating label selection sensitivity. 

## Next Steps 
2026-03-20

- expand the dataset to include a wider range of threat intelligence scenarios  
- refine zero-shot candidate labels to improve classification accuracy  
- test cybersecurity-specific models trained on security datasets  
- explore combining model outputs into a single relevance score  
- evaluate integration with real-time data sources instead of static samples  
