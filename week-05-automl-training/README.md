# Week 5: AutoML & No-Code Model Training

Implemented and evaluated a text classification pipeline and compared generic vs fine-tuned Hugging Face models for the Relevance Scorer component of the Intelligence Threat Dashboard.

## Custom Model Training
- Built a phishing vs legitimate text classifier using TF-IDF vectorization and Naive Bayes
- Evaluated performance on a held-out test set
- Accuracy: 100%
- Precision: 100% | Recall: 100% | F1 Score: 100%

Note: Results are based on a small dataset and may not generalize to real-world data. Future improvements would include expanding the dataset with more diverse phishing and legitimate examples to enhance generalization and reduce overfitting.

## Fine-Tuned Model Comparison 
Compared 3 models (1 generic + 2 fine-tuned) on 5 test inputs:
 - Generic: distilbert-sst-2 (sentiment)
 - Fine-Tuned A: cardiffnlp twitter-roberta-base-sentiment-latest
 - Fine-Tuned B: papluca/xlm-roberta-base-language-detection

## Finding
Recommended cardiffnlp/twitter-roberta-base-sentiment-latest for the Relevance Scorer because it provides more meaningful analysis of linguistic patterns such as urgency and tone, which are relevant for identifying suspicious or phishing-related content.

Fine-tuned models showed more consistent and interpretable outputs, but results highlighted that models not trained on cybersecurity-specific data struggle to correctly classify threat indicators. 

## Notes
- Generic sentiment models failed to capture cybersecurity context
- Fine-tuned models improved consistency but still lacked domain-specific understanding
- Model performance is highly dependent on training data alignment

See report.md for full analysis.