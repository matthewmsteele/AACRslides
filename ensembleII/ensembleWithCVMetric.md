Ensembling Proceedure with CV Metrics
========================================================
author: 
date: 
autosize: true

Previously . . .
========================================================

*In an effort to improve score modeling performance:*

 - New individual classifier ensembling proceedures were considered that leverage classification probability
 
 - It was suggest that weighting on individual classifer cross validation metrics be considered

Which CV Metric?
========================================================

*Problem:*
There are lots of ways to evaluvte classification algorithm performance. What metric should use for weighting?

**Proposal:**
Select metric that provides a pair of values; 
(probability that prediction of this type are correct, probability that prediction of this type is incorrect)

Which CV Metric?
========================================================

**Proposal:**
Select metric that provides a pair of values; 
(probability that prediction of this type are correct, probability that prediction of this type is incorrect)

*This would allow weighting using combination of probability estimates of based on algorithm "confidence" individual response scoring and model performance*

Which CV Metric?
========================================================

**Proposal:**
Select metric that provides a pair of values; 
(probability that prediction of this type are correct, probability that prediction of this type is incorrect)

Positive:  \( \sum_{\rm{Algorithms}} P_{\rm{Prediction}}(+) P_{\rm{Performance}}(+)  > \sum_{\rm{Algorithms}} P_{\rm{Prediction}}(-) P_{\rm{Performance}}(-) \)


Which CV Metric?
========================================================


|         |Negative |Positive |
|:--------|:--------|:--------|
|Negative |TN       |FN       |
|Positive |FP       |TP       |

Postive Preiction: (Positive Prediction Value = TP/(TP+FP), False Omission Rate = FN/(TN+FN))

Negative Prediction: (False Discovery Rate = FP/(TP+FP), Negative Prediction Value= TN/(TN+FN))

Which CV Metric? Alternate
========================================================

**Proposal:**
Select metric that provides a pair of values; 
(probability that prediction of this type are correct, probability that prediction of this type is incorrect)

Positive: \( \sum_{\rm{Algorithms}} P_{\rm{Prediction}}(+)^a P_{\rm{Performance}}(+)^b  > \sum_{\rm{Algorithms}} P_{\rm{Prediction}}(-)^a P_{\rm{Performance}}(-)^b \)

Testing: Weight Loss
========================================================

N=1175

Cross Validation Kappa Values

| Human| Simple| Prob Weighted| PLR L2| Prob + CV|
|-----:|------:|-------------:|------:|---------:|
|   385|  0.955|         0.957|  0.956|     0.957|
|    10|  0.181|         0.459| -0.002|     0.011|
|    99|  0.387|         0.512|  0.621|     0.655|
|   478|  0.695|         0.707|  0.733|     0.723|
|    10|  0.000|         0.000|  0.000|     0.000|
|   219|  0.857|         0.880|  0.889|     0.880|

Testing: Root Cell
=========================================================

N=677
Cross Validation Kappa Values

| Human| Simple| Prob Weighted| PLR L2| Prob + CV|
|-----:|------:|-------------:|------:|---------:|
|   175|  0.795|         0.827|  0.809|     0.840|
|   127|  0.812|         0.838|  0.828|     0.833|
|    69|  0.738|         0.755|  0.681|     0.786|
|   139|  0.878|         0.908|  0.895|     0.903|
|   110|  0.580|         0.608|  0.610|     0.634|



Testing: Grape
========================================================

N=317

Cross Validation Kappa Values

| Human| Simple| Prob Weighted| PLR L2| Prob + CV|
|-----:|------:|-------------:|------:|---------:|
|   161|  0.861|         0.905|  0.905|     0.886|
|    56|  0.712|         0.813|  0.814|     0.902|
|    28|  0.364|         0.509|  0.680|     0.900|
|    62|  0.562|         0.671|  0.774|     0.768|
|    67|  0.630|         0.694|  0.740|     0.777|

Testing: Non-coding Mutation
=========================================================

N=301
Cross Validation Kappa Values

| Human| Simple| Prob Weighted| PLR L2| Prob + CV|
|-----:|------:|-------------:|------:|---------:|
|   224|  0.729|         0.727|  0.706|     0.724|
|   183|  0.818|         0.795|  0.768|     0.788|
|    35|  0.734|         0.779|  0.755|     0.898|
|    45|  0.427|         0.531|  0.489|     0.658|
|    38|  0.596|         0.652|  0.525|     0.761|
|    55|  0.835|         0.861|  0.824|     0.861|
|    38|  0.422|         0.475|  0.300|     0.619|


