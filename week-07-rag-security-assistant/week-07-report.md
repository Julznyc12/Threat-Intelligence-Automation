# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## 1. Setup Summary

- **LLM:** llama-3.3-70b-versatile via Groq  
- **Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace  
- **Vector Store:** In-Memory Vector Store  
- **Documents loaded:**  
  - mitre-initial-access.txt (~1–2 pages)  
  - mitre-credential-access.txt (~1–2 pages)  
  - mitre-lateral-movement.txt (~1–2 pages)  

---

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
|---|----------|----------------|---------|-------|
| 1 | What are common techniques for credential access? | Yes | Good | Accurately referenced Credential Dumping and Brute Force techniques |
| 2 | How does phishing relate to initial access in ATT&CK? | Yes | Good | Clearly explained phishing as an initial access method using document content |
| 3 | What is lateral movement and what techniques do attackers use? | Yes | Good | Correctly described lateral movement and referenced Remote Services and Pass the Hash |
| 4 | What does the NIST framework recommend for the Detect function? | No | Good | Correctly indicated lack of information without hallucinating |
| 5 | What is the difference between spearphishing attachment and spearphishing link? | Partial | Partial | Answer was related but did not fully distinguish due to limited document detail |

---

## 3. Edge Case Observations

- **Unrelated question:**  
When asked an unrelated question (e.g., weather), the chatbot either declined to answer or indicated it did not have relevant information. This demonstrates that the RAG system is properly constrained by its knowledge base.

- **Topic not in documents:**  
When asked about topics not included in the uploaded documents (e.g., NIST Detect function), the chatbot responded with uncertainty rather than generating incorrect information. This indicates minimal hallucination and proper retrieval behavior.

---

## 4. Settings Experiments (if completed)

- **Temperature change:**  
Increasing the temperature resulted in slightly more varied and less deterministic responses. Lower temperature (0.3) produced more factual and consistent answers, which is preferable for a security knowledge assistant.

- **Chunk size change:**  
Reducing chunk size improved retrieval precision but slightly reduced context in responses. Larger chunk sizes provided more context but could introduce less relevant information.

- **Top K change:**  
Adjusting Top K affected how many document chunks were retrieved. Lower values made responses more focused, while higher values included broader context but sometimes added unnecessary details.

---

## 5. Reflection

- **What surprised you about how RAG works?**  
What stood out was how effectively the system limits responses to only the provided documents. Instead of relying purely on the LLM’s general knowledge, the chatbot retrieves relevant context first, which significantly improves accuracy and trustworthiness.

- **How could you improve this chatbot for real-world use?**  
The chatbot could be improved by adding more comprehensive and diverse documents, using a persistent vector database (such as Pinecone or Chroma), and refining chunking strategies. Additional improvements could include better prompt engineering and integrating real-time data sources.

- **How might you use RAG in your capstone project?**  
RAG could be used to support the relevance scoring process within a threat intelligence feed dashboard by providing contextual explanations for incoming alerts and intelligence data. As a relevance scorer, the system could assist in determining whether a piece of threat intelligence is meaningful or actionable by retrieving related information from known frameworks such as MITRE ATT&CK. For example, when evaluating an alert or intelligence entry, the RAG system could provide supporting context about associated techniques, helping to assess its significance and prioritize it appropriately. This would improve the accuracy and consistency of relevance scoring and support more informed decision-making within the dashboard.

---