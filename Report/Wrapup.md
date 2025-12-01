# Conclusion

-   saying each model posed a solution to one of the drawbacks of finBERT - scale/ runtime; lack of topic sentiment; numerical reasoning
-   how each model scales
-   real-world applications - difficulty finding a large enough labelled dataset makes unsupervised techniques more appropriate
-   for current dataset, distilBERT is best (smaller so works better on smaller dataset) - finBERT tended to overfit

## Section 2 - finBERT

Attempting to fine-tune the finBERT model for this data set consisted of a number of challenges due to the imbalance of the classes and the size of the data set which is small relatively small compared to the number of parameters in the finBERT model - which resulted in a highly overfitted model. We attempted to solve these problems through regularization (such as weight decay) and by using a weighted loss function. Whilst this helped to prevent over fitting it did so by sacrificing some performance (reduction in accuracy across classes) and it was difficult to optimize to find a balance due to the limited compute and long training times (\~1 hour).

Furthermore whilst finBERT has been trained on financial language it sometimes reverted back to relying on lexical sentiment rather than financial sentiment to make predictions, (eg classifying "Unemployment rate jumps" as positive because "jump" is a positive verb). In addition, as finBERT is a NLP it hasn't been trained for numerical reasoning and so it struggles to compare two numbers unless there is a lexical sentiment indicator such as "increased" or "decreased".

Finally, finBERT uses a standard cross-entropy loss which treats each label as independent of the other. However, there is a natural order to the labels which, given more time, would have been good to fine-tune for. By using an ordinal loss function such as CORAL we could discourage large mistakes (eg predicting negative for a positive case) by punishing more severely based off the "distance" between true and predicted labels.

# More compute/ larger dataset

With greater compute, we could fine-tune more extensively, unfreezing additional layers, performing multi-stage training, or training larger variants (e.g., RoBERTa-large FinBERT). This would improve granularity while still avoiding over fitting.
