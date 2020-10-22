---
title: GoogleNet 簡介與小實驗
date: 2020-10-23 07:15:00
tags: [ai, deep learning, googlenet, pytorch, python]
des: "本文簡單介紹 GoogLeNet，並分享我亂改造 GoogLeNet 模型的實驗結果。"
---

## 介紹

GoogLeNet 最早是發表在 Google 的 Paper：[Going deeper with convolutions](https://arxiv.org/pdf/1409.4842.pdf)，裡面介紹了 Inception V1/GoogLenet 架構，並在 ILSVRC-2014 比賽中在分辨項目第一名(Top-5 Error=6.67%)，他只有約 6.8 百萬個參數，比 AlexNet 少九倍，更比 VGG-16 少二十倍，也就是說 GoogleNet 的模型更為輕巧。

本文簡單介紹 GoogLeNet，並分享我亂改造 GoogLeNet 模型的實驗結果。

## GoogLeNet 模型介紹

在多數情況下我們不清楚何時何地該使用 Max-pooling 和 Convolution，所以 GoogLeNet 乾脆一次全都用，他同時將不同大小的 Kernel 的 Convolution 連同 Max-pooling，Concatenate 輸出成 Output，此稱作 Inception 模組，而整個 GoogLeNet 就是許多 Inception 模組所組成。

![GoogLeNet](https://user-images.githubusercontent.com/18013815/96935484-bd937500-14f6-11eb-9c1e-a87e2050bef4.png)

上圖即為 Inception 模組示意圖，GoogLeNet 還有一個創意是提出 Bottleneck 的概念，可以看到左邊是一般的 Inception 模組，而右邊是改造過的，裡面引入 1x1 Convolution，藉由 1x1 Conv 我們可以大量減少參數，故稱為 Bottleneck。

![GoogLeNet Inception Parameters](https://user-images.githubusercontent.com/18013815/96935814-75c11d80-14f7-11eb-9a73-70d52ce63e1d.png)

在沒有使用 Bottleneck 情況下，MAC (Multiply–Accumulate Operation) 數量是 $((28\times 28\times 5\times 5)\times 192)\times 32 ≃ 120$。

反之在有 1x1 Conv 幫忙縮減之下，MAC 變成第一層 $((28\times 28\times 1\times 1)\times 192)\times 16 ≃ 2.4M$ 加上第二層 $((28\times 28\times 5\times 5)\times 16)\times 32 ≃ 10M $，總共約為 $12.4M$。所以可以觀察到 MAC 大約可以減少十倍左右的計算量，而事實上整個模型參數也大約減少十倍。

![GoogLeNet Architecture](https://user-images.githubusercontent.com/18013815/96936889-7fe41b80-14f9-11eb-8159-ffd97a34bd91.png)

上圖示整個 GoogLeNet 的架構圖，大致上來說就是有九個 Inception Module。

![GoogLeNet Parameter Table](https://user-images.githubusercontent.com/18013815/96937010-cafe2e80-14f9-11eb-8e33-d787171acff9.png)

架構的細節配置參考上表。

## Pytorch 實作 GoogLeNet

程式碼沒有很長，就直接全貼上來了，基本上就是將 Pytorch 範例中的 MNIST 拿來用，並使用 [pytorch-cifar100](https://github.com/weiaicunzai/pytorch-cifar100) 專案中的 GoogLenet 模組。

Copy 以下程式碼，應該就可以直接執行了，我的環境是 Python3 + Pytorch 1.6 + Cuda 10.2。

<details>

```python
from __future__ import print_function
import argparse
import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
import torchvision
from torchvision import transforms
from torch.optim.lr_scheduler import StepLR
import numpy as np

class Inception(nn.Module):
    def __init__(self, input_channels, n1x1, n3x3_reduce, n3x3, n5x5_reduce, n5x5, pool_proj):
        super().__init__()

        # 1x1conv branch
        self.b1 = nn.Sequential(
            nn.Conv2d(input_channels, n1x1, kernel_size=1),
            nn.BatchNorm2d(n1x1),
            nn.ReLU(inplace=True)
        )

        # 1x1conv -> 3x3conv branch
        self.b2 = nn.Sequential(
            nn.Conv2d(input_channels, n3x3_reduce, kernel_size=1),
            nn.BatchNorm2d(n3x3_reduce),
            nn.ReLU(inplace=True),
            nn.Conv2d(n3x3_reduce, n3x3, kernel_size=3, padding=1),
            nn.BatchNorm2d(n3x3),
            nn.ReLU(inplace=True)
        )

        # 1x1conv -> 5x5conv branch
        # we use 2 3x3 conv filters stacked instead
        # of 1 5x5 filters to obtain the same receptive
        # field with fewer parameters
        self.b3 = nn.Sequential(
            nn.Conv2d(input_channels, n5x5_reduce, kernel_size=1),
            nn.BatchNorm2d(n5x5_reduce),
            nn.ReLU(inplace=True),
            nn.Conv2d(n5x5_reduce, n5x5, kernel_size=3, padding=1),
            nn.BatchNorm2d(n5x5, n5x5),
            nn.ReLU(inplace=True),
            nn.Conv2d(n5x5, n5x5, kernel_size=3, padding=1),
            nn.BatchNorm2d(n5x5),
            nn.ReLU(inplace=True)
        )

        # 3x3pooling -> 1x1conv
        # same conv
        self.b4 = nn.Sequential(
            nn.MaxPool2d(3, stride=1, padding=1),
            nn.Conv2d(input_channels, pool_proj, kernel_size=1),
            nn.BatchNorm2d(pool_proj),
            nn.ReLU(inplace=True)
        )

    def forward(self,\times):
        return torch.cat([self.b1(x), self.b2(x), self.b3(x), self.b4(x)], dim=1)


class GoogleNet(nn.Module):

    def __init__(self, num_class=100):
        super().__init__()
        self.prelayer = nn.Sequential(
            nn.Conv2d(3, 192, kernel_size=3, padding=1),
            nn.BatchNorm2d(192),
            nn.ReLU(inplace=True)
        )

        # although we only use 1 conv layer as prelayer,
        # we still use name a3, b3.......
        self.a3 = Inception(192, 64, 96, 128, 16, 32, 32)
        self.b3 = Inception(256, 128, 128, 192, 32, 96, 64)

        # """In general, an Inception network is a network consisting of
        # modules of the above type stacked upon each other, with occasional
        # max-pooling layers with stride 2 to halve the resolution of the
        # grid"""
        self.maxpool = nn.MaxPool2d(3, stride=2, padding=1)

        self.a4 = Inception(480, 192, 96, 208, 16, 48, 64)
        self.b4 = Inception(512, 160, 112, 224, 24, 64, 64)
        self.c4 = Inception(512, 128, 128, 256, 24, 64, 64)
        self.d4 = Inception(512, 112, 144, 288, 32, 64, 64)
        self.e4 = Inception(528, 256, 160, 320, 32, 128, 128)

        self.a5 = Inception(832, 256, 160, 320, 32, 128, 128)
        self.b5 = Inception(832, 384, 192, 384, 48, 128, 128)

        # input feature size: 8*8*1024
        self.avgpool = nn.AdaptiveAvgPool2d((1, 1))
        self.dropout = nn.Dropout2d(p=0.4)
        self.linear = nn.Linear(1024, num_class)

    def forward(self,\times):
        output = self.prelayer(x)
        output = self.a3(output)
        output = self.b3(output)

        output = self.maxpool(output)

        output = self.a4(output)
        output = self.b4(output)
        output = self.c4(output)
        output = self.d4(output)
        output = self.e4(output)

        output = self.maxpool(output)

        output = self.a5(output)
        output = self.b5(output)

        # """It was found that a move from fully connected layers to
        # average pooling improved the top-1 accuracy by about 0.6%,
        # however the use of dropout remained essential even after
        # removing the fully connected layers."""
        output = self.avgpool(output)
        output = self.dropout(output)
        output = output.view(output.size()[0], -1)
        output = self.linear(output)

        return output


def train(args, model, device, train_loader, optimizer, epoch):
    model.train()
    for batch_idx, (data, target) in enumerate(train_loader):
        data, target = data.to(device), target.to(device)
        optimizer.zero_grad()
        output = model(data)
        loss = F.cross_entropy(output, target)
        loss.backward()
        optimizer.step()
        if batch_idx % args.log_interval == 0:
            print('Train Epoch: {} [{}/{} ({:.0f}%)]\tLoss: {:.6f}'.format(
                epoch, batch_idx * len(data), len(train_loader.dataset),
                100. * batch_idx / len(train_loader), loss.item()))
            if args.dry_run:
                break


def test(model, device, test_loader):
    model.eval()
    test_loss = 0
    correct = 0

    top5count = 0

    with torch.no_grad():
        for data, target in test_loader:
            data, target = data.to(device), target.to(device)
            output = model.forward(data)

            v, result = output.topk(5, 1, True, True)
            top5count += torch.eq(result, target.view(-1, 1)
                                  ).sum().int().item()

            # sum up batch loss
            test_loss += F.cross_entropy(output,
                                         target, reduction='sum').item()
            # get the index of the max log-probability
            pred = output.argmax(dim=1, keepdim=True)
            correct += pred.eq(target.view_as(pred)).sum().item()

    test_loss /= len(test_loader.dataset)

    print('\nTest set: Average loss: {:.4f}, Top 1 Error: {}/{} ({:.2f}), Top 5 Error: {}/{} ({:.2f})\n'.format(
        test_loss,
        len(test_loader.dataset) - correct, len(test_loader.dataset),
        1 - correct / len(test_loader.dataset),
        len(test_loader.dataset) - top5count, len(test_loader.dataset),
        1 - top5count / len(test_loader.dataset),
    ))


def main():
    # Training settings
    parser = argparse.ArgumentParser(description='PyTorch MNIST Example')
    parser.add_argument('--batch-size', type=int, default=64, metavar='N',
                        help='input batch size for training (default:   64)')
    parser.add_argument('--test-batch-size', type=int, default=10, metavar='N',
                        help='input batch size for testing (default: 10)')
    parser.add_argument('--epochs', type=int, default=14, metavar='N',
                        help='number of epochs to train (default: 14)')
    parser.add_argument('--lr', type=float, default=1.0, metavar='LR',
                        help='learning rate (default: 1.0)')
    parser.add_argument('--gamma', type=float, default=0.7, metavar='M',
                        help='Learning rate step gamma (default: 0.7)')
    parser.add_argument('--no-cuda', action='store_true', default=False,
                        help='disables CUDA training')
    parser.add_argument('--dry-run', action='store_true', default=False,
                        help='quickly check a single pass')
    parser.add_argument('--seed', type=int, default=1, metavar='S',
                        help='random seed (default: 1)')
    parser.add_argument('--log-interval', type=int, default=10, metavar='N',
                        help='how many batches to wait before logging training status')
    parser.add_argument('--save-model', action='store_true', default=False,
                        help='For Saving the current Model')
    args = parser.parse_args()
    use_cuda = not args.no_cuda and torch.cuda.is_available()

    torch.manual_seed(args.seed)

    device = torch.device("cuda:0")

    train_kwargs = {'batch_size': args.batch_size}
    test_kwargs = {'batch_size': args.test_batch_size}
    if use_cuda:
        cuda_kwargs = {'num_workers': 2,
                       'pin_memory': True,
                       'shuffle': True}
        train_kwargs.update(cuda_kwargs)
        test_kwargs.update(cuda_kwargs)

    transform = transforms.Compose(
        [transforms.RandomHorizontalFlip(p=0.5),
         transforms.ToTensor(),
         transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])

    trainset = torchvision.datasets.CIFAR100(root='./data', train=True,
                                             download=True, transform=transform)
    trainloader = torch.utils.data.DataLoader(trainset, **train_kwargs)

    testset = torchvision.datasets.CIFAR100(root='./data', train=False,
                                            download=True, transform=transform)
    testloader = torch.utils.data.DataLoader(testset, **test_kwargs)

    model = GoogleNet().to(device)
    optimizer = optim.Adadelta(model.parameters(), lr=args.lr)

    scheduler = StepLR(optimizer, step_size=1, gamma=args.gamma)
    for epoch in range(1, args.epochs + 1):
        train(args, model, device, trainloader, optimizer, epoch)
        test(model, device, testloader)
        scheduler.step()

    if args.save_model:
        torch.save(model.state_dict(), "mnist_cnn.pt")

    model_parameters = filter(lambda p: p.requires_grad, model.parameters())
    params = sum([np.prod(p.size()) for p in model_parameters])
    print("Parameters:", params)


if __name__ == '__main__':
    main()
```

</details>

## GoogLeNet 的小實驗

接著我跑了一些實驗來看 GoogLeNet 的表現，首先包含有 Bottleneck 的 GoogLeNet，以及沒有的 Naïve GoogLeNet。除此之外我將原本 GoogLeNet 隨意加了兩層 Inception 稱為 GoogLeNet Long，並且隨意減少 Inception Layer 稱作 GoogLeNet Short，被我刪減最多的是 GoogLeNet Short4，裡面只剩下兩層 Inception。幾本上可以從 Parameters 數量去大概了解模型大小。

我使用這幾個模型去跑 CIFAR100 和 CIFAR10 資料集，並記錄 Top1 Error, Top5 Error, Parameters, Time。


**GoogLeNet 執行 CIFAR100**：

|                         |     Top   1 Error     |     Top 5 Error    |     Parameters    |     Time(14 epoch)    |
|-------------------------|-----------------------|--------------------|-------------------|-----------------------|
|     GoogleNet Naïve     |     0.36              |     0.09           |     65736148      |     52m38s            |
|     GoogleNet           |     0.34              |     0.10           |     6258500       |     29m8s             |
|     GoogleNet Long      |     0.35              |     0.10           |     9641924       |     36m41s            |
|     GoogleNet Short     |     0.32              |     0.09           |     5271652       |     23m11s            |
|     GoogleNet Short2    |     0.32              |     0.09           |     3523556       |     16m29s            |
|     GoogleNet Short3    |     0.36              |     0.11           |     1985220       |     9m3s              |
|     GoogleNet Short4    |     0.44              |     0.15           |     1650084       |     8m56s             |

**GoogLeNet 執行 CIFAR10**：

|                         |     Top   1 Error     |     Top 5 Error    |     Parameters    |     Time(14 epoch)    |
|-------------------------|-----------------------|--------------------|-------------------|-----------------------|
|     GoogleNet Naïve     |     0.15              |     0.01           |     65291098      |     52m51s            |
|     GoogleNet           |     0.10              |     0.00           |     6166250       |     28m45s            |
|     GoogleNet Long      |     0.11              |     0.00           |     9549674       |     40m12s            |
|     GoogleNet Short     |     0.10              |     0.00           |     5179402       |     27m30s            |
|     GoogleNet Short2    |     0.10              |     0.00           |     3431306       |     31m57s            |
|     GoogleNet Short3    |     0.11              |     0.00           |     1892970       |     26m31s            |
|     GoogleNet Short4    |     0.15              |     0.01           |     1557834       |     25m30s            |

首先我們可以看到 Parameters 確實 Naïve 多了十倍，但是模型的 Accuracy 並沒有差異太大。此外可以看到除了 Short4 以外幾乎所有模型的結果都差不多，CIFAR100 基本上都在 Top 1 Error 0.35 & Top 5 Error 0.10 左右，而 CIFAR10 基本上都在 Top 1 Error 0.10 & Top 5 Error 0.00 (近乎零) 左右。

我猜這是因為 CIFAR100 和 CIFAR10 不夠複雜的緣故，所以對於圖片辨識來說，模型的深度影響就還好了，此外除了模型深度，Channel 數量也會對正確度有影響，如果 Channel 數量夠大，也許就不需要太深的網路。我也嘗試在 GoogleNet 裡面亂加 Max-Pooling Layer 和 Dropout Layer，基本上 Error 都大同小異，可見在圖片辨識上模型本身的容錯率應該是滿高的。

不過以上實驗的推論僅適用簡單的測試集，在複雜的測試集中，模型本身造成的幾 % 正確度都非常重要，僅僅是小數點的差異就藏著無數的心血和巧思。不過 GoogleNet 最厲害的地方還是省去了一大堆參數，正確度卻幾乎差不多！
