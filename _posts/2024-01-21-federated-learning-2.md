---
layout: post
title: Machine Learning Perspective
categories: [FederatedLearning, English]
---


### Deep Neural Networks

- In the each party, the approach is same as traditional ML.
- Things to consider for Federated Learning
  - Batch Size selection
  - Local Epochs are run before aggregrates? should all parties use for each epochs?
  - how to choose learning rate for each party. difference in data distribution
- there are some commnucation overhade when we aggregate one party for each.
  - we can do concurrently, or **FedAvg**

#### FedAvg

- each party runs multiple epochs before replying to aggregator.
- parties compute new set of weights directly at each party, and reply with their model with number of samples.
- preforms well in different model type.

For each Federated Learning approach that addresses specific aspect of data heterogeneity, model structure, and parties. Need to defind algorithm with *Local trainig function, Fusion Function, and protocol for interation between parties and aggregator*

### Classical Machine Learning Models

Classical machine learning can also be applied to FL.

#### Linear Models

- regression, classification can be trained in FL simliar to the DNN method.
- FedAvg . Federated SGD can be used.
- often converges fater since w is smaller than DNN.
- logistic regression and linear SVN can also be federated learning approach

#### Decision Tree

- require different approach to FL compare to linear and DNN because it is classification model type.
- explainaility of decision is important in healthcare, finance other relgulated industry.
- no good fusion algorithm have been proposed to merge independently trained tree model into single decision tree.
- For ID3 algorithm FL version, tree formation takes place at the aggregator and parties will count to the proposed class splits based on their local training data.
  - works for numeric and categorical data.
- aggregator is prominent role and perfoms almost all computation, yet parties provides counts to feature and split values.
- Depending on quantity of training dataset and number of class pamber, it need privacy-preserving measures to ensure not too much information is disclosed in this simple approach.

#### Decision Tree ensemble method

- random forest, gradient boosted tree(XGBoost), are successufully used in different application.
- Federated random forest will be simliar to Fedeated decision tree.
  - other algorithm can handle all parties does not have same set of feature for each data record. Vertical Federated Learning and requires cryptographic techonique to match the record.
- Greadient-Boosted Tree aggregatore create tree growth and decision making like other federated learning tree.
  - federated gradient-boosted tree can have good accuracy and have less overfitted than other trees.
  - use party-adaptive quantile to reduce information disclosure.
  - use cryptographic method to secure multi-party computation approach and loss computation.
  - higher training time. more privacy.
  
### Horizontal, Vertical Federated Learning and Split Learning

- we usally assume that all parties training data has same feature for sample and different sample. like we assume each party has sample of equivalent size and content.
- **But**, there are many data that aren't. So we can partition by vertically.

![image1](/images/federatedLearning/federatedlearning_2-1.png)

- Create Key to match with other partition, but need cryptography.

- Split learning is partitioned between client and server. ex DNN
  - client maintains Upper part of DNN down to split layer
  - server has split layer and the rest.
  - client has data and server has label.

### Model Personalization

- adaption of globel model to the data distribution of speicfic parties participating in FL Process.
- personalize the final model respected by the speicfic party can have better outcome.
- ex, individual parties can run additional local training epochs on local data at the end of FL process.
- 3 different personalization: user clustering, training on interpolated data(global and local), model interpolation
  - user clustering : need less strict privacy requirement or better privacy techo to cluster user on training data
  - data interpolation : based on creation of a global dataset.
  - model interpolation: is the widest applicability from a privacy perspective.
    - ex, a method to optimize averaging a global model and a local model for personalizeation purpose by determining optimized weight. 
    