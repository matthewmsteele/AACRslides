Ensembling Procedure
========================================================
author: 
date: 

Ensemble of Classifcation Algorithms
========================================================

![Ensemble Procedure](ensemble.png)

The Problem
========================================================

__Individual algorithms perform better/worse on certain types of prompt/rubric pairs__

One Solution:
 - Manually select which algorithms to use in the ensemble
 
The Problem with the Solution
========================================================

Good, except for:
 - Manual selection challenging and time consuming
 - Even lesser algorithms contribute when used in aggregate
 
Another Solution
========================================================
 
__A Smarter Ensembling Proceedure__
 
Let the system select (or bettering yet assign weights to) the individual classifiers during the training of a scoring model
 
Current Solution: Simple Voting
========================================================

![Ensemble Procedure](ensemble.png)

One Better: Leverage Scoring Probability
========================================================

![Ensemble Procedure](ensemble2.png)

First Approach: Probabilty Weighted Voting
========================================================

__Select the score with the highest aggregate probability__

Example: 3 Algorithms with positive/negative classification


|         | Algorithm 1| Algorithm 2| Algorithm 3| Total|
|:--------|-----------:|-----------:|-----------:|-----:|
|Postive  |        0.52|        0.55|         0.3|  1.37|
|Negative |        0.48|        0.45|         0.7|  1.63|

Probabilty Weighted Voting
========================================================
__Select the score with the highest aggregate probability__

_Pros_
 - Fast/Cheap/Simple
 - Leverages self reported probabilities
 
_Cons_
 - Leverages self reported probabilites

A Second Approach: Ensembling Classifier
========================================================
__Fit a secondary classifier that uses probabilites as features__

A secondary classifier would:
 - Select which algorithms to use as input
 - Weight the input classifiers based on predictive power
 - Utalize probabilities in a more sofisticated manner
 
A Second Approach: Ensembling Classifier
========================================================
__Fit a secondary classifier that uses probabilites as features__

Caveats
 - More computationally intense
 - Reduce the amount of data availible to primary classifiers
 
More Specifically: Penalized Logistic Regression
========================================================

__Penalized Logistic Regression__
 - Logistic regression with weighting
 - Designed to minimized overfitting with lots of features
 - Effectively limits influence of features with low predictive power 

Limitations of Current System
========================================================
__In the current implementation each individual a score and an associated probability__

Example: Data returned by a single classifier for a 3 level holistic rubric

| Score| Probability|
|-----:|-----------:|
|     1|        0.95|
|     3|        0.83|
|     2|        0.43|
|     1|        0.67|
|     1|        0.87|

Limitations of Current System
========================================================
__In the current implementation each individual a score and an associated probability__

To construct a complete feature set for this example we would need probabilites

| Bin 1| Bin 2| Bin 3|
|-----:|-----:|-----:|
|  0.95|  0.02|  0.03|
|  0.33|  0.40|  0.27|
|  0.13|  0.72|  0.15|
|  0.07|  0.05|  0.88|
|  0.67|  0.21|  0.12|

Limitations of Current System
========================================================

__*Thus* within current framework either weighted voting or PLR ensembling may only be performed with on analytic rubrics with positive/negtive coded bins__

Limitations of Current System
========================================================

__*Thus* within current framework either weighted voting or PLR ensembling may only be performed with on analytic rubrics with positive/negtive coded bins__

These limits are *not* tied to the algorithms, but to the implementation

Testing: Weight Loss
========================================================

N=1175

Cross Validation Kappa Values

| Human| Simple| Weighted| PLR L2| PLR L1|
|-----:|------:|--------:|------:|------:|
|   385|  0.955|    0.957|  0.956|  0.956|
|    10|  0.181|    0.459| -0.002|  0.000|
|    99|  0.387|    0.512|  0.621|  0.586|
|   478|  0.695|    0.707|  0.733|  0.727|
|    10|  0.000|    0.000|  0.000|  0.000|
|   219|  0.857|    0.880|  0.889|  0.886|

Testing: Root Cell
=========================================================

N=677
Cross Validation Kappa Values

| Human| Simple| Weighted| PLR L2| PLR L1|
|-----:|------:|--------:|------:|------:|
|   175|  0.795|    0.827|  0.809|  0.805|
|   127|  0.812|    0.838|  0.828|  0.803|
|    69|  0.738|    0.755|  0.681|  0.626|
|   139|  0.878|    0.908|  0.895|  0.884|
|   110|  0.580|    0.608|  0.610|  0.606|



Testing: Grape
========================================================

N=317

Cross Validation Kappa Values

| Human| Simple| Weighted| PLR L2| PLR L1|
|-----:|------:|--------:|------:|------:|
|   161|  0.861|    0.905|  0.905|  0.912|
|    56|  0.712|    0.813|  0.814|  0.812|
|    28|  0.364|    0.509|  0.680|  0.595|
|    62|  0.562|    0.671|  0.774|  0.791|
|    67|  0.630|    0.694|  0.740|  0.800|

Testing: Non-coding Mutation
=========================================================

N=301
Cross Validation Kappa Values

| Human| Simple| Weighted| PLR L2| PLR L1|
|-----:|------:|--------:|------:|------:|
|   224|  0.729|    0.727|  0.706|  0.693|
|   183|  0.818|    0.795|  0.768|  0.762|
|    35|  0.734|    0.779|  0.755|  0.800|
|    45|  0.427|    0.531|  0.489|  0.493|
|    38|  0.596|    0.652|  0.525|  0.583|
|    55|  0.835|    0.861|  0.824|  0.794|
|    38|  0.422|    0.475|  0.300|  0.208|


Preliminary Results
==========================================================

__Leveraging prediction $\Longrightarrow$ higher performance models__

 - **Probability Weighted Voting preferred** for under sampled feature space; more data is better
 - **PLR preferred** well sampled feature space; identifying best predictors better
 - No clear preferred PLR penalty structure

