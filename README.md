# Functional Metrics
Uses combination of IDF and BLEU-score concept

## Problem Statement
The existing Direct and Fuzzy match metrics don’t add a functional value
A metric needs to be defined to evaluate the model’s extraction in relation to the functional relevance

## Approach
Given Actual and Predicted, remove low impact words (link) from both the strings (using Normalization table)
    Ex: Law, Office, LLP etc

```
For each k-grams where k is in [2, max_ngrams] :
    Get k-grams of continuous chars in actual and predicted. 
    Check how many are matching 
    Compare the number of matching k-grams against total k-grams in Actual (Recall) and total k-grams in Predicted (Precision)
    Take maximum of precision and recall
Take average of the maximum scores across all k-grams
```

### Example:
```
Actual - Sedgwick; Predicted - Sedgvic
For k in range(2, max_ngrams):
    No. of k-grams in GT (se, ed, dg, gw, wi, ic, ck) = 7
    No. of k-grams in Pred (se, ed, dg, dv, vi, ic) = 6
    No. of Correctly predicted - (se, ed, dg, ic) = 4
    Precision = 4/6, Recall = 4/7
    max_score = 0.67
Return average of all max_score
```