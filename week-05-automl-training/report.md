Name: Julian Silva Erazo

Date: 3/26/2026

Capstone Project: Intelligence Threat Dashboard

My Component: Relevance Scorer

## Part A: Teachable Machine Training (Text Classification Alternative)

### Training Setup
- Task: Phishing vs Legitimate Text Classification
- Training images per class: ~20 phishing, ~20 legitimate (text samples)
- Test images per class: 4 phishing, 4 legitimate
- Total training time: ~30 seconds

### Test Results 
| # | Actual Class | Predicted Class | Confidence | Correct? |
| - | ------------ | --------------- | ---------- | ---------|
| 1 | phishing     | phishing        | 0.76       | ✅        |
| 2 | legitimate   | legitimate      | 0.76       | ✅        |
| 3 | phishing     | phishing        | 0.75       | ✅        |
| 4 | legitimate   | legitimate      | 0.53       | ✅        |
| 5 | phishing     | phishing        | 0.74       | ✅        |
| 6 | legitimate   | legitimate      | —          | ✅        |
| 7 | phishing     | phishing        | —          | ✅        |
| 8 | legitimate   | legitimate      | —          | ✅        |


### Confusion Matrix 
|                        | Predicted: Phishing | Predicted: Legitimate |
| ---------------------- | ------------------- | --------------------- |
| **Actual: Phishing**   | TP = 4              | FN = 0                |
| **Actual: Legitimate** | FP = 0              | TN = 4                |

### Calculated Metrics
- Accuracy: 100%
- Precision: 100%
- Recall: 100%
- F1 Score: 100%

### Interpretation 
The model achieved perfect accuracy, precision, and recall on the test set; however, this result is likely due to the small dataset size and limited number of test samples. With only eight test examples, the model may be overfitting and may not generalize well to real-world phishing detection scenarios. Increasing both the size and diversity of the dataset would improve the model’s generalization and its ability to handle more complex, real-world inputs.

## Part B: Generic vs Fine-Tuned Model Comparison 

### Models Tested
1. Generic: distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. Fine-Tuned A: cardiffnlp/twitter-roberta-base-sentiment-latest — a fine-tuned RoBERTa-based sentiment classification model used to detect urgency, negative tone, and emotionally manipulative language commonly associated with phishing and social engineering attacks.
3. Fine-Tuned B: papluca/xlm-roberta-base-language-detection — language detection model used to identify anomalies in communication patterns

### Results
| Input                           | Generic Label (Score) | Fine-Tuned A Label (Score) | Fine-Tuned B Label (Score) | Best Model   |
| ------------------------------- | --------------------- | -------------------------- | -------------------------- | ------------ |
| Unauthorized login from IP...   | POSITIVE (0.7481)     | legitimate (0.8441)        | legitimate (0.9918)        | Fine-Tuned A |
| Routine firewall rule update... | POSITIVE (0.7481)     | legitimate (0.8743)        | legitimate (0.9918)        | Fine-Tuned A |
| Phishing email with spoofed...  | POSITIVE (0.7481)     | legitimate (0.5479)        | legitimate (0.9918)        | Fine-Tuned A |
| Multiple failed SSH attempts... | POSITIVE (0.7481)     | legitimate (0.8144)        | legitimate (0.9918)        | Fine-Tuned A |
| System resource utilization...  | POSITIVE (0.7481)     | legitimate (0.6699)        | legitimate (0.9918)        | Fine-Tuned A |


### Analysis

Generic model strengths:
The generic sentiment model provided consistent outputs and served as a baseline for comparison. It was easy to integrate and produced stable confidence scores across all inputs.

Generic model weaknesses:
The model failed to capture cybersecurity context, labeling all inputs as positive regardless of whether they described suspicious or potentially malicious activity. This demonstrates poor domain alignment with security-related text.

Fine-tuned model advantage:
The fine-tuned sentiment model (Model A) provided more meaningful interpretation by analyzing tone and linguistic patterns, which can reflect urgency or suspicious intent. While it still classified inputs as legitimate, it showed more variation in confidence scores, making it more useful for ranking or prioritizing messages in a relevance scoring system.

Biggest surprise:
The most surprising result was that all models classified clearly suspicious inputs as legitimate. This highlights the limitation of using models trained on general or non-cybersecurity datasets, as they lack awareness of technical threat indicators such as unauthorized access attempts or phishing-related behavior. 

These results demonstrate that while fine-tuned models improve performance over generic baselines, domain-specific training is essential for accurate threat detection in cybersecurity scenarios. 

## Recommended Model for My Capstone Component

Component: Relevance Scorer

Primary model:
Fine-Tuned A: cardiffnlp/twitter-roberta-base-sentiment-latest — This model is the most effective for the relevance scorer because it captures urgency and negative tone, which are common characteristics of phishing attempts and suspicious communications. 

Confidence threshold:
0.80 — Predictions above this threshold would be automatically flagged as relevant, while lower-confidence results would be routed for human review to reduce false positives and maintain accuracy.

Priority metric:
Recall — Recall is the most important metric for the relevance scorer because missing a relevant or suspicious threat related message is far more critical than reviewing additional false positives. This ensures important signals are not overlooked within an intelligence workflow. 

---

## Limitations & Next Steps

One major limitation is that the models used were not trained on cybersecurity-specific datasets, which caused them to misclassify technical alerts and threat-related inputs. The models were unable to properly interpret events such as unauthorized logins or failed SSH attempts due to a lack of domain alignment. 

With more time, I would build a labeled dataset consisting of real phishing emails, SOC alerts, and threat intelligence reports, and fine-tune a model specifically for the Intelligence Threat Dashboard. I would also test additional cybersecurity-focused models and evaluate their performance based on recall and false-negative rates to improve the effectiveness of the relevance scoring system.
