---
title: "[Paper Review] Deep learning"
date: 2020-10-21 23:34:00
tags: [paper, machine learning, deep learning, inference, ai]
des: "A short review of the paper, Deep learning, Nature 2015."
---

## Paper Information

**Paper**: Deep learning
**Author**: Yann LeCun, Yoshua Bengio & Geoffrey Hinton 
**Source**: [Nature 2015](https://www-nature-com.ezproxy.lib.nctu.edu.tw/articles/nature14539)

## Review

This paper is a review paper that briefly introduces the development of Deep Learning.

It first demonstrates supervised learning, which requires a lot of labeled data to train the model. The purpose of supervised learning is to modify its internal adjustable parameters to increase accuracy. To achieve the goad, stochastic gradient descent (SGD) has been proposed, which give a little noise to the steps for estimation, and surprisingly get a fast training time with good weight parameters.

The paper discusses classifiers then. The linear classifiers can only recognize targets in simple domains. Shallow classifiers require good feature extractors to solve the selectivity. Kernel methods may sound like a good idea to concur with the selectivity problem but resulting in a higher requirement of engineering and domain knowledge. However, non-linear problems are still hard. Following the thoughts, a deep learning architecture comes out, which has multiple non-linear layers so that it can handle non-linear inputs and outputs. There are two ways to deal with the deep neural network (DNN), forward propagation, and backpropagation. The last one runs faster. With ReLU non-linear function, the DNN learns much faster in a model with many layers, because its computation is simple.

Training a model usually requires abundant time, but if we choose a pre-training model with many trained layers, and just re-training by only add a layer in the original model, we can train the model fast. It’s also useful when we only have a small amount of labeled data.

Convolutional neural networks (CNN) is a very successful model. Its key points are local connections, shared weights, pooling, and the use of many layers. CNN achieves the highest success in image recognition, such a face recognition. With ReLU, dropout, and deforming the existing data to new ones, CNN has even better performance.

![CNN example](https://user-images.githubusercontent.com/18013815/96743614-c735b380-13f6-11eb-8f6d-ab6595be8bc5.png)
(CNN example)

CNN is powerful; however, it doesn’t do well in streaming-like data inputs, such as video, neural language, sound processing. It’s because CNN lacks memories in networks. Reinforcement neural networks (RNN) appears. RNN can remember the history of the data, for example, the long short-term memory (LSTM) networks, a kind of RNN, use hidden units called memory cells to remember some information longer. RNN does well, especially on NLP.

We can expect deep learning will keep developing fast, and it can be used everywhere, resulting in a better world with AI.
