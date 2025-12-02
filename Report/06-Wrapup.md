# Conclusion

-   saying each model posed a solution to one of the drawbacks of finBERT - scale/ runtime; lack of topic sentiment; numerical reasoning
-   how each model scales
-   real-world applications - difficulty finding a large enough labelled dataset makes unsupervised techniques more appropriate
-   for current dataset, distilBERT is best (smaller so works better on smaller dataset) - finBERT tended to overfit

## Section 2 - finBERT

Attempting to fine-tune the finBERT model for this data set consisted of a number of challenges due to the imbalance of the classes and the size of the data set which is small relatively small compared to the number of parameters in the finBERT model - which resulted in a highly overfitted model. We attempted to solve these problems through regularization (such as weight decay) and by using a weighted loss function. Whilst this helped to prevent over fitting it did so by sacrificing some performance (reduction in accuracy across classes) and it was difficult to optimize to find a balance due to the limited compute and long training times (\~1 hour).

Furthermore whilst finBERT has been trained on financial language it sometimes reverted back to relying on lexical sentiment rather than financial sentiment to make predictions, (eg classifying "Unemployment rate jumps" as positive because "jump" is a positive verb). In addition, as finBERT is a NLP it hasn't been trained for numerical reasoning and so it struggles to compare two numbers unless there is a lexical sentiment indicator such as "increased" or "decreased".

Finally, finBERT uses a standard cross-entropy loss which treats each label as independent of the other. However, there is a natural order to the labels which, given more time, would have been good to fine-tune for. By using an ordinal loss function such as CORAL we could discourage large mistakes (eg predicting negative for a positive case) by punishing more severely based off the "distance" between true and predicted labels.

## Section 3 - FinGPT

Through our exploration of FinGPT, we investigated whether a modern, instruction-tuned LLM could outperform a traditional transformer like FinBERT on financial sentiment classification. While FinGPT is theoretically more capable—particularly in its ability to process numerical context, capture multi-step reasoning, and interpret financial statements—our experiments highlighted several practical limitations that prevented these advantages from being fully realised.

The most significant barrier was computational. Fine-tuning a 20B-parameter model requires access to a high-end data-centre GPU, without which the model cannot be trained or even loaded efficiently. This stands in contrast to FinBERT, which is lightweight enough to be trained on consumer hardware and therefore far more accessible for real-world experimentation.

Beyond compute, FinGPT introduces complexity that FinBERT avoids. As a generative LLM, it requires prompt formatting, output control, and additional evaluation steps to ensure consistent label predictions—adding engineering overhead without guaranteeing better performance on a small and imbalanced dataset. Its scale also increases the risk of overfitting and makes hyperparameter tuning much more sensitive, meaning the dataset used here is not ideally suited to exploiting its capabilities.

Overall, while FinGPT offers the potential for richer financial understanding than FinBERT, these strengths can only be leveraged with significant computational resources and a much larger corpus of training data. In applied settings, this makes FinBERT the more practical choice, whereas FinGPT represents a powerful but resource-intensive alternative whose benefits may only emerge under far more favourable training conditions.

## Section 4 - LDA
Through the implementation of LDA combined with dictionary-based scoring, we successfully developed an unsupervised sentiment pipeline capable of detecting thematic market signals without reliance on labeled training data. While our evaluation confirmed that the FinBERT model yields superior classification accuracy, the LDA approach achieved a critical objective that FinBERT cannot: Interpretability. By decomposing sentiment into topics, the LDA model transforms a 'Black Box' prediction into an explainable audit trail, which is a regulatory necessity in real-worl financial applications. Furthermore, our experimentation revealed that LDA struggles with the nuance of 'Neutral' sentiment (it often simply acted as a binary filter for extreme news) which, given more time, could be more deeply studied and resolved with some adjustments to the data pre-processing. Therefore an interesting and natural extension of our analysis could be using the strenghts of both LDA and Finbert together i.e. using LDA to explain the 'why' behind FinBERT's 'what'.


# More compute/ larger dataset

With greater compute, we could fine-tune more extensively, unfreezing additional layers, performing multi-stage training, or training larger variants (e.g., RoBERTa-large FinBERT). This would improve granularity while still avoiding over fitting.
The methods presented in the LDA notebook include many scalability solutions whilst the use of LDA in itself is already a much faster and less computationally costly approach than usuing FinBERT. Hence LDA-based methods could be preferred to Neural Network methods like FinBERT if minimising time and compute cost is essential but in a setting where high performance is more desirable, the results of this project conclude that FinBERT remains the better choice. 
