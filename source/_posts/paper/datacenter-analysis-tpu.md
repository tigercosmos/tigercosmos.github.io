---
title: "[Paper Review] In-Datacenter Performance Analysis of a Tensor Processing Unit"
date: 2020-12-03 23:46:00
tags: [paper, machine learning, tpu, deep learning, performance analysis, ai]
des: "A short review of the paper, In-Datacenter Performance Analysis of a Tensor Processing Unit."
---

## Paper Information

**Paper**: In-Datacenter Performance Analysis of a Tensor Processing Unit
**Author**: Norman P. Jouppi et al.
**Source**: [ISCA '17: Proceedings of the 44th Annual International Symposium on Computer Architecture](https://dl-acm-org.ezproxy.lib.nctu.edu.tw/doi/10.1145/3079856.3080246)


## Review

TPU (Tensor Processing Unit) is the state-of-art neural network accelerator designed by Google, which arms with a 65536 8-bit MAC (multiplier–accumulator) unit that offers a peak throughput of 92 TeraOps/second (TOPS) and a large (28 MiB) software-managed on-chip memory. In this paper, the authors from Google want to gain a deeper understanding of the performance of in-datacenter TPU for common deep learning usage by analyzing the data collected from their datacenters.

The first interesting thing is about 95% of the TPU workload is about MLP (Multi-Layer Perceptrons) and LSTM. It is surprising because CNN is usually considered as the common layer in neural networks.
![table 1](https://user-images.githubusercontent.com/18013815/101040675-29b5ce00-35b7-11eb-8d25-7a9145ab4137.png)

The following three figures are the TPU's design. The most important parts are the **matrix multiply unit** and the **large unified buffer**, which affect the operations of the neural network the most since most models are memory-bound and many layers execute matrix multiplication. TPU was designed to be a coprocessor on the PCIe I/O bus, and it doesn't fetch instructions to run, in contrast, the host server sends TPU instructions for it to execute. Since the PCIe bus is relatively slow, TPU instructions follow the **CISC** tradition. The CISC `MatrixMultiply` instruction is 12 bytes, and the philosophy of the TPU is to keep the matrix unit as busy as possible. A four-stage pipeline is used by TPU.

<div align='center' style="width: 60%">

![figure 1](https://user-images.githubusercontent.com/18013815/101042090-bf515d80-35b7-11eb-8f07-00719aa75176.png)
![figure 2](https://user-images.githubusercontent.com/18013815/101042118-c7110200-35b7-11eb-9b34-bb6f9a74636a.png)
![figure 3](https://user-images.githubusercontent.com/18013815/101042156-cf693d00-35b7-11eb-8fc3-cf251404e759.png)

</div>


A given matrix MAC operations move through the matrix as a **diagonal wavefront**, since the performance is affected by the latency of the matrix unit. This is shown in the following figure.

<div align=center>
<img src="https://user-images.githubusercontent.com/18013815/101044220-10fae780-35ba-11eb-8924-941f3c2a42ad.png" alt="figure 4" width=50%>
</div>

The platforms used in the experiment are listed in the following table.
![table 2](https://user-images.githubusercontent.com/18013815/101044562-7058f780-35ba-11eb-8786-ce6e5e331cbd.png)

To evaluate the performance of the six applications (2 MLPs and 2 LSTMs are memory-bound but only the 2 CNNs are compute-bound) on the three processors (TPU, GPU, CPU), the **Roofline Performance Model** from high-performance computing is adapted. The explanation in the paper is so clear that I would rather like to cite its sentences:

> The assumption behind the model is that applications don’t fit in on-chip caches, so they are either computation-limited or memory bandwidth-limited. For HPC, the Y-axis is the performance in floating-point operations per second, thus the peak computation rate forms the “flat” part of the roofline. The X-axis is operational intensity, measured as floating-point operations per DRAM byte accessed. Memory bandwidth is bytes per second, which turns into the “slanted” part of the roofline since (FLOPS/sec)/ (FLOPS/Byte) = Bytes/sec. Without sufficient operational intensity, a program is memory bandwidth-bound and lives under the slanted part of the roofline.

The following graph combines the three processors' performance for each app.
![figure 8](https://user-images.githubusercontent.com/18013815/101046050-b2cf0400-35bb-11eb-9f44-2f8e1523b37f.png)

TPU's **ridge point** is far to the right to 1350 multiply-accumulate operations per byte of weight memory read, which is far away from CPU and GPU, which explains the advantage of TPU's memory size. For TPU (start points), 2 LSTMs and 2 MLPs are under the slanted part of the roofline, which means memory bandwidth is the bottleneck for them, and the peak computations rate of TPU limits the performance of 2 CNNS.

For GPU (triangle points), most of the points are under the roofline, which stands for the DNN performance is limited by the **response time**. Despite increasing the throughput to reducing the response time, it also decreases the workload sent to GPU. The performance of the CPU does not stand in stark contrast to the one of GPU, which is really unexpectedly due to many factors like response time or memory size. Overall, all points of GPU and CPU are far below to TPU's, which shows the high performance of TPU.

To sum up, TPU leverages 25 times MACs and 3.5 times on-chip memory to K80 GPU, and only costs half the power of the K80. The larger memory helps increase the operational intensity of DNN models to fully utilize the MACs capacity, making it competitive to others accelerators. In addition, CNNs only count 5% of the NN workload in datacenters, which suggests that the focus should be put on MLPs and LSTMs more.
