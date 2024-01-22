---
layout: post
title: Overview, Concepts and Terminology
categories: [FederatedLearning, English]
---

### What and why Federated Learning

- training data is not managed locally.
- data is not shared with other entity.
- ML depends on the availiability of high-quality training data.
- data privacy has many regulations like HIPAA
- Federated Learning can be conducted without data stored centralized.
- It was created because of different regulations in different nations/regions.

### How Federated Learning works?

> a set ouf distinct parties, controls respective training data and collaborate to train a machine learning model without sharing data.

![image1](/images/federatedLearning/federatedlearning_1.png)
![image1](/images/federatedLearning/federatedlearning_2.png)


1. Aggregator uses function Q takes input model from previous round, M~t-1 at round t and generates q~t for current round.
    1. M~0 can be emtpy or randomly generated, Federated Learning algorithm may include additional input for function Q and tailer to each party.
2. Aggregator sends query q~t to parties and request for information of parties local model or aggregated information.
    1. ex, queries includes requests for gradients or model weights of a neural network, or counts for decision trees.
3. When receiving query q~t, parties locally train based on their private data, Dk, send their model parameters to the aggregator as model updates(r~k,t).
    1. query q~t contains information that the party can initialize local training process.
        1. ex, model weights of the new commone model M~t to initialize local training, or other information for different model types.
    2. updates will be different from the type of machine learning models
        1. ex, the update will be weight of the network for neural network.
4. When local training function L is completed, r~k,t is sent back from party p~k to the aggregator A, collects all r_k,t from all parties.
5. Aggregator recives all model updates R~t = (r~1,t, r~2,t ... r~n,t) merges to common model once it recives all updates from parties. (model fusion F)
    1. ex, can be simple of averaging weight(FedAvg Algo) for neural network.
6. Merged model M~t destributed to the parties for next round of learning, repeating until traning process converges.
    1. ex, also manually set number of round is possible but it is highly vary(from Naive Bayes approach to gradient-based machine learning)
7. Final model that trained from all parties without sharing data.

#### Local training function, fusion function, query generation function

- Are typically complimentary set
- L interacts with actual dataset and performs local training, generates r~k,t
- F gets input of R~t, create next model M~t
- Q will be created for next round.

### Distributed Learning VS Federated Learning

- Similiar
  - Using Server(aggregator) to aggregate the results from nodes, trained with distributed data.
- Different
  - Distribution and quantity of data is **not** controlled in FL.
  - Cannot assume IID of data in parties.
    - some parties will have more data and others.

> must aware of Imbalance and non-IIDness of data.

#### Number of Parties in FL

- Enterpries/Cross-silo use case
  - ex, traning model on datasets in different data centers of multi-national company(<10 parties)
  - generally important for all data from all/most parties
  - FL process considers the identity of the parties invovle, and can use for training and verification.
  - Communication failure can be managed because of less parties.
- Cross-device usecase
  - ex, traning model is from mobile phone application.(hundereds of millions parties)
  - only include a -potentially large- sub-sample of the total set of devices.
  - party identity is not important, single partiy might be involved in one training.
  - Because devices can have communication failure, need to mitigate by sampling parties and setting up time limit to perform aggregation or more
  - Q determines not only queries but alsy which parties will be included for next round.
    - ex, can be randomized, by party characteriestics
    - F need to integrate with different queries for new model M~t.
  
### Alternative FL Architectures

- every party P~k may have their associated aggregatore A~k, querying the other parties.
- set of parties might be partitioned between aggregatores
- hiierachical aggregation process may take place.

#### Terms

##### Party p~k

- clients or devices(ex, smart phone, car, wearables, cloud services like data centers, embedded systems such as manufacturing robots)

##### Aggregator A

- Facilitates the collaboaration.
- to coordinate the learning process and information exchange between parties and to perform into common model,

##### Model M

- represents a predictive function f on training data D.
- can have the structure of neural network or any other non-neural model.

##### Data D

- constrast to centralized ML, D is partitioned between n parties P = {P~1, P~2 .. P~n} where each party P~k are subset of P.
- P owns a private training dataset D~k

##### Local trainig function L

##### Fusion function F

##### Query generation function Q

##### Model Updates r~k,t