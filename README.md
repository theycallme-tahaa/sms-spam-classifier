# SMS Spam Classifier

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/theycallme-tahaa/sms-spam-classifier/blob/main/sms_spam_classifier.ipynb)

A machine learning project that classifies text messages as **spam** or **ham** (legitimate), using Python and scikit-learn.

## Overview

- **Data:** [SMS Spam Collection](https://archive.ics.uci.edu/dataset/228/sms+spam+collection) (UCI), about 5,500 labelled English SMS messages
- **Features:** TF-IDF on word unigrams and bigrams, with English stop words removed
- **Models:** Multinomial Naive Bayes and Logistic Regression
- **Evaluation:** precision, recall, F1, confusion matrix and 5-fold stratified cross-validation

Accuracy alone is misleading on this dataset, because most messages are ham. So the notebook focuses on precision and recall for the spam class, and on the cost of each kind of mistake: a real message wrongly flagged as spam is worse than a spam message that gets through.

## Results

| Naive Bayes | 98.3% | 98.5% | 88.6% | 93.3% |
| Logistic Regression | 97.5% | 89.5% | 92.0% | 90.7% |

Cross-validated F1: **0.939 ± 0.017** (Naive Bayes) 
                    **0.931 ± 0.011** (Logistic Regression)

## Run it

**On your phone or in the browser:** tap the "Open in Colab" badge above, then choose *Runtime → Run all*. No installation needed.

**On a computer:**

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
jupyter notebook sms_spam_classifier.ipynb
```

The notebook downloads the dataset automatically, so you need an internet connection on first run.

## What's in the notebook

1. Load the data
2. Explore it (class balance, message length)
3. Stratified train/test split
4. TF-IDF + Naive Bayes, with a confusion matrix
5. Logistic Regression and a side-by-side comparison
6. Cross-validation to check the result is stable
7. The words each class relies on most
8. Predictions on new messages
9. Results, limitations and next steps

## Limitations

- Small, English-only and fairly old dataset, so modern scams may be missed
- The model reads only the words in a message, not links, sender or timing
- It would need retraining as spam changes over time

## Next steps

- Character n-grams and hand-made features (digit count, currency symbols, capital-letter ratio)
- Tune the decision threshold to favour precision
- Wrap the model in a small web app

## What I learned

Naive Bayes has very high precision (98.5%). When it flags a message as spam, it’s almost always right, so it rarely sends a real message to the spam folder.
Logistic Regression has higher recall (92.0% vs 88.6%). It catches more spam, but at the cost of more false alarms (precision 89.5%).
Which is better depends on the goal. Most people hate losing a real message more than seeing a stray spam, so Naive Bayes is the safer choice here, and it also scores slightly higher in cross-validation.
Accuracy is high for both (98.3% and 97.5%), but it hides these differences. This is why precision and recall matter.
