---
layout: post
title: What is Federated Learning?
categories: [FederatedLearning, English]
---


- training data is not managed locally.
- data is not shared with other entity.
- ML depends on the availiability of high-quality training data.
- data privacy has many regulations like HIPAA
- Federated Learning can be conducted without data stored centralized.
- It was created because of different regulations in different nations/regions.

## How Federated Learning works?

> a set ouf distinct parties, controls respective training data and collaborate to train a machine learning model without sharing data.

![image1](/images/federatedLearning/federatedlearning_1.png)

1. Parties locally train based on their private data, send their model parameters to the aggregator as model updates.
    1. updates will be different from the type of machine learning models
        1. ex, the update will be weight of the network for     neural network.
2. Aggregator merges to common model once it recives all updates from parties. (model fusion)
    1. ex, can be simple of averaging weight(FedAvg Algo) for neural network.
3. Merged model destributed to the parties for next round of learning, repeating until traning process converges.
4. Final model that trained from all parties without sharing data.

## Distributed Learning VS Federated Learning

- Similiar
  - Using Server(aggregator) to aggregate the results from nodes, trained with distributed data.
- Different
  - Distribution and quantity of data is **not** controlled in FL.
  - Cannot assume IID of data in parties.
    - some parties will have more data and others.

> must aware of Imbalance and non-IIDness of data.

### Number of Parties in FL

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

### terms

#### Party

- clients or devices(ex, smart phone, car, wearables, cloud services like data centers, embedded systems such as manufacturing robots)

#### Aggregator

- Facilitates the collaboaration.
- to coordinate the learning process and information exchange between parties and to perform into common model,
