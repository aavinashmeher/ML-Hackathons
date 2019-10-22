<h2> Amazon ML Hiring challenge </h2>
<h3> Problem Description </h3>

Given Review Text and Review Title predict which topic/category it belongs to.

<h4> Sample Data: </h4>

|Review Text|Review Title|Topic|
|-----------|------------|-----|
|Did nothing for me, didn't help lost even with working out and eating healthy. Didn't curb appetite or anything.|Useless|Shipment and delivery|
|Gave me an allergic reaction on my face :(|Do not recommend|Allergic|

<h3> My Approach: </h3>

1. After preprocessing the Review Text and Review Title concatenated both of these features to create TFIDF features with min_df=0.005.
2. Trained Logistic Regression with 3 fold Stratified cross-validation to get Accuracy of 0.5682.
3. Trained XGBClassifier with 2 fold Stratified cross-validation to get Accuracy of 0.5542.
4. Trained a simple LSTM model with embedding layer and dropouts to get Accuracy of 0.6174:-
    - Constructed word embeddings leveraging a pretrained GLOVE model for the Embedding layer.
    - Choose Dropout rate = 0.2 for the Dense layers.
