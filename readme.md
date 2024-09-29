# Alzheimer's Disease Diagnosis

Binary classifier trained on the [Alzheimer's Disease Dataset](https://www.kaggle.com/datasets/rabieelkharoua/alzheimers-disease-dataset) for educational purposes.

Features were selected by means of univariate statistical tests. 

Stratified 10-fold cross-validation, repeated 10 times, was carried out on a variety of algorithms. For each of them, a grid search was also performed with a nested stratified 10-fold cross-validation, in order to find the optimal hyper-parameters. 

Hyper-parameters were tuned with the objective of optimizing the F1-score. This metric was chosen as the target over the accuracy, because of the class imbalance in the dataset favoring the negative examples: optimizing the balance between the precision (proportion of positive predictions that are actually correct) and the recall (proportion of positive examples that have been identified) makes the model less biased towards the negative classifications. To this end, the cost of false negatives (misclassification of positive examples as negative examples) was also tuned during grid search, when cost-sensitive learning was supported by the algorithm.

The most promising learning schemes resulted being those corresponding with the decision tree and random forest algorithms, with the latter slightly surpassing the former on all metrics in a statistically significant manner. However, these differences are very small, especially on the final models (fit on the entire training set), which agreement is 0.98 (according to their Cohen's kappa). It follows that the decision tree may be preferred for a matter of interpretability.

<img src="tree.png" />

```
|--- FunctionalAssessment <= 4.97
|   |--- ADL <= 5.04
|   |   |--- MMSE <= 24.02
|   |   |   |--- class: 1
|   |   |--- MMSE >  24.02
|   |   |   |--- class: 0
|   |--- ADL >  5.04
|   |   |--- MemoryComplaints <= 0.50
|   |   |   |--- BehavioralProblems <= 0.50
|   |   |   |   |--- class: 0
|   |   |   |--- BehavioralProblems >  0.50
|   |   |   |   |--- MMSE <= 23.79
|   |   |   |   |   |--- class: 1
|   |   |   |   |--- MMSE >  23.79
|   |   |   |   |   |--- class: 0
|   |   |--- MemoryComplaints >  0.50
|   |   |   |--- MMSE <= 23.92
|   |   |   |   |--- class: 1
|   |   |   |--- MMSE >  23.92
|   |   |   |   |--- class: 0
|--- FunctionalAssessment >  4.97
|   |--- MemoryComplaints <= 0.50
|   |   |--- BehavioralProblems <= 0.50
|   |   |   |--- class: 0
|   |   |--- BehavioralProblems >  0.50
|   |   |   |--- ADL <= 5.04
|   |   |   |   |--- MMSE <= 23.99
|   |   |   |   |   |--- class: 1
|   |   |   |   |--- MMSE >  23.99
|   |   |   |   |   |--- class: 0
|   |   |   |--- ADL >  5.04
|   |   |   |   |--- class: 0
|   |--- MemoryComplaints >  0.50
|   |   |--- MMSE <= 23.15
|   |   |   |--- ADL <= 4.99
|   |   |   |   |--- class: 1
|   |   |   |--- ADL >  4.99
|   |   |   |   |--- BehavioralProblems <= 0.50
|   |   |   |   |   |--- class: 0
|   |   |   |   |--- BehavioralProblems >  0.50
|   |   |   |   |   |--- class: 1
|   |   |--- MMSE >  23.15
|   |   |   |--- class: 0
```