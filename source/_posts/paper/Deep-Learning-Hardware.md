---
title: "[Paper Review] Deep Learning Hardware: Past, Present, and Future"
date: 2020-10-21 23:46:00
tags: [paper, machine learning, deep learning hardware, ai]
des: "A short review of the paper, Deep Learning Hardware: Past, Present, and Future."
---

## Paper Information

**Paper**: Deep Learning Hardware: Past, Present, and Future
**Author**: Yann LeCun, et al.
**Source**: [2019 IEEE International Solid- State Circuits Conference (ISSCC)](https://ieeexplore-ieee-org.ezproxy.lib.nctu.edu.tw/document/8662396)


## Review

This paper is a review paper that briefly introduces the development of the Deep Learning and the Hardware for Deep Learning from past to future.

We know that there are two neural network winters before. The reason that we can conquer the second winter is 4 factors: improved methods, big data, advanced accelerators, and open source libraries. In the past, people never thought about a “deep” neural network. It was not because the people were not smart enough, but because of the limitation of the processors. Now we have fast GPGPU, FPGA, DLA, TPU, etc., so the devices are never the bottleneck of deep learning. By the advance of the devices, people can create more and more methods of building and training models.

The hardware is of importance for deep learning. As the Chinese saying goes: “A worker needs a good tool to do his job.” Deep learning computations are always heavy, so we have to rely on the processing speed of the devices. The author categorizes five cases about hardware requirements: DL research, off-line training for products, inference on servers, inference on mobile devices, and on-line learning on servers or mobiles. For different usage, we focus on different topics, such as we don’t care about off-line training because we only care about the accuracy of the model; or, we cut off the model size and use only 16-bits or 8-bits floating-point number for mobile devices.

The author also indicates the idea of self-supervised learning (SSL) is more efficient than reinforcement learning and supervised learning. He introduces one of the SSL technique—Generative Adversarial Networks (GAN), which has an inspiring performance. The SSL is good at prediction, so the author guesses it is the future of the intelligent systems for robotic and autonomous driving.

At last, the author discusses the future of DL software and hardware. There are many DL compilers, so there comes to ONNX. Sparse activation is one of the features that makes the brain so power-efficient. Low-power ASICs for DL is also a trend.
