---
title: 電腦動畫中的反向動力法 (Inverse Kinematics)
date: 2020-06-09 00:00:00
tags: [電腦動畫, 反向動力法, computer animation, inverse kinematics, jacobian, pseudo inverse]
des: "在電腦動畫或機器人學中，我們可能會希望一個人物或機器人做到特定的動作，例如伸手能碰到手把或伸手接到球。如果以正向動力學的方式去推敲怎樣達到我們想要的姿勢幾乎不可能。這時候就會採用反向動力學，當我們給物件目標位置後，用反推的方式算出物件如何運動可以達到該位置。"
---

## 1. 介紹

在電腦動畫或機器人學中，我們可能會希望一個人物或機器人做到特定的動作，例如伸手能碰到手把或伸手接到球。

一個物件可能會有很多關節，假設每個關節都是 5 個維度 (DoF)，一個手臂假設是三段關節，那就會是 15 個維度，如果以正向動力學 (Forward Kinematics, FK) 的方式去推敲怎樣達到我們想要的姿勢幾乎不可能。

這時候就會採用反向動力學 (Inverse Kinematics, IK)，當我們給物件目標位置後，用反推的方式算出物件如何運動可以達到該位置。

![ik example](https://user-images.githubusercontent.com/18013815/84060735-4cdc3800-a9ef-11ea-878b-dafc5233ff5e.gif)
(用 IK 算出怎樣讓手臂動到目標位置)

反向動力學通常要解一個高維的問題，造成它十分難算，需要花費大量運算且可以有很多種解。常見的方法包含 Cyclic Coordinate Descent 方法、Jacobian Pseudoinverse 方法、Jacobian Transpose 方法、Levenberg-Marquardt Damped Least Squares 方法、Quasi-Newton and Conjugate Gradient 方法、神經網路方法。

根據所需的計算時間、精準度、反推的動作姿勢等需求，在做 IK 時也會選不同的方法，例如 Cyclic Coordinate Descent 都會是指尖先動才去動手臂，Jacobian Pseudoinverse 則會一次動所有關節，神經網路則可以快速預判和做出比較擬真的結果。而本文將介紹反向動力法的 Jacobian Pseudoinverse 方法。

## 2. Jacobian Pseudoinverse 原理與實作

### 2.1 參數定義

假設有一個機械手臂，我們希望他的手指可以動到特定位置，並設定從手指到手臂中間的每個關節的初始位置 $\mathbf s_i$ 都會轉動，透過中間這些關節運動，使得手指可以達到目標位置 $\mathbf t$。

<img src="https://i.imgur.com/coqDQA1.jpg" width="80%">


定義有 $n$ 維度的世界座標，$n$ 通常是 3，代表 $x, y, z$ 三個維度，但也可以轉成其他維度空間。

第 $i$ 個關節的初始位置向量表示為：

$$ 
\mathbf s_i = 
    \begin{bmatrix}
s_x & s_y &s_z & \dots & s_n
    \end{bmatrix}
$$

目標位置向量為：

$$ 
\mathbf t = 
    \begin{bmatrix}
t_x & t_y &t_z & \dots & t_n
    \end{bmatrix}
$$

定義第 $i$ 個關節的 End Effector $\mathbf e$：

$$\mathbf e_i = \mathbf t - \mathbf s_i$$

所以每個關節的 End Effector 向量表示為：


$$ 
\mathbf e = 
    \begin{bmatrix}
e_1 & e_2 &e_3 & \dots & e_N
    \end{bmatrix}
$$



對於所有關節包含的所有 $M$ 個可動維度 (DoF) 的旋轉角度向量為：

$$ 
\mathbf \theta = 
    \begin{bmatrix}
\theta_1 & \theta_2 & \theta_3 & \dots & \theta_M
    \end{bmatrix}
$$

### 2.2 動力學

在正向動力法 (Forward Kinematics) 中，可以由已知的轉動角度，透過 $f$ 函數算出下一步的 End Effector $e$，我們有以下算式：

$$\mathbf e = f(\mathbf \theta)$$


在反向動力學中 (Inverse Kinematics) 中，我們將關係反過來，我們給定 End Effector，希望得到旋轉的角度：

$$\mathbf \theta = f^{-1}(\mathbf e)$$

### 2.3 Jacobian

向量微積分的 [Jacobian](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant) 代表一個函數 $f$ 的線性近似值，我們可以用 Jacobian $J$ 從 End Effector $\mathbf e$ 去回推 d$\mathbf \theta$。

<img src="https://i.imgur.com/z22VM1L.jpg" width="80%">


<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mrow class="MJX-TeXAtom-ORD"><mi mathvariant="bold">J</mi></mrow><mo>=</mo><mrow class="MJX-TeXAtom-ORD"><mfrac><mrow class="MJX-TeXAtom-ORD"><mi>d</mi><mrow class="MJX-TeXAtom-ORD"><mi mathvariant="bold">e</mi></mrow></mrow><mrow class="MJX-TeXAtom-ORD"><mi>d</mi><mrow class="MJX-TeXAtom-ORD"><mi>&#x03B8;<!-- θ --></mi></mrow></mrow></mfrac></mrow></math>

$$d\mathbf e  = \mathbf J d \mathbf \theta$$

$\mathbf J$ 表示成：

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"> <mrow class="MJX-TeXAtom-ORD"> <mi mathvariant="bold">J</mi> </mrow> <mo>=</mo> <mrow> <mo>(</mo> <mtable rowspacing="4pt" columnspacing="1em"> <mtr> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>1</mn> </msub> </mrow> <mrow> <mi>d</mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>1</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>1</mn> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>2</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mo>&#x22EF;<!-- ⋯ --></mo> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>1</mn> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mi>n</mi> </msub> </mrow> </mfrac> </mtd> </mtr> <mtr> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>2</mn> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>1</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>2</mn> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>2</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mo>&#x22EF;<!-- ⋯ --></mo> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mn>2</mn> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mi>n</mi> </msub> </mrow> </mfrac> </mtd> </mtr> <mtr> <mtd> <mo>&#x22EE;<!-- ⋮ --></mo> </mtd> <mtd> <mo>&#x22EE;<!-- ⋮ --></mo> </mtd> <mtd> <mo>&#x22EF;<!-- ⋯ --></mo> </mtd> <mtd> <mo>&#x22EE;<!-- ⋮ --></mo> </mtd> </mtr> <mtr> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mi>k</mi> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>1</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mi>k</mi> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mn>2</mn> </msub> </mrow> </mfrac> </mtd> <mtd> <mo>&#x22EF;<!-- ⋯ --></mo> </mtd> <mtd> <mfrac> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>f</mi> <mi>k</mi> </msub> </mrow> <mrow> <mi mathvariant="normal">&#x2202;<!-- ∂ --></mi> <msub> <mi>&#x03B8;<!-- θ --></mi> <mi>n</mi> </msub> </mrow> </mfrac> </mtd> </mtr> </mtable> <mo>)</mo> </mrow></math>

回顧我們剛剛得到 $d\mathbf e  = \mathbf J d \mathbf \theta$，我們移項得到：

$$ d\mathbf \theta  = \mathbf J^{-1} d \mathbf e$$

這個旋轉角度變化量 $d\mathbf \theta$ 就是我們想得到的，因為我們可以用 $d\mathbf \theta$ 去回推上一步的位置。

<img src="https://i.imgur.com/ZP2mRyp.jpg" width="80%">


### 2.4 求 Jacobian 近似解


定義世界座標是三維度 (3 DoF)，為解 $d\mathbf \theta  = \mathbf J^{-1} d \mathbf e$ 我們需要先求 Jacobain。以下算式都是建立在世界座標之下。

先看 Jacobian 的其中一欄：

$$
\mathbf J_i =
\frac{\partial \mathbf e}{d\theta_1}=
\begin{bmatrix}
\frac{\partial e_{x}}{\partial\theta_i} \\\\
\frac{\partial e_{y}}{\partial\theta_i} \\\\
\frac{\partial e_{z}}{\partial\theta_i}
\end{bmatrix}
$$

取 $\mathbf \theta$ 和 $\mathbf e$ 的線性微小變化量來近似偏微分：

$$
\mathbf J_i =
\frac{\partial \mathbf e}{d\theta_i}=
\frac{\Delta \mathbf e}{\Delta\theta_i}=
\begin{bmatrix}
\frac{\Delta e_{x}}{\Delta\theta_i} \\\\
\frac{\Delta e_{y}}{\Delta\theta_i} \\\\
\frac{\Delta e_{z}}{\Delta\theta_i}
\end{bmatrix}
$$

對於某關節 $A$ 的**其中一維度**的旋轉，該維度下，關節 $A$ 的 End Effector $\mathbf e$ 的線性的變化 $d\mathbf e$，等於關節 $A$ 在此維度下旋轉的變化量 ($\mathbf \omega \mathbf rdt$)。

$$
\frac{d\mathbf e}{dt} = 
\vert \mathbf \omega \vert {\frac{\mathbf \omega}{\vert \mathbf \omega \vert }} \times \mathbf r =
\frac{d \mathbf \theta}{dt} \mathbf a \times \mathbf r
$$

其中 $\mathbf a= \frac{\mathbf \omega}{\vert \omega \vert}$，代表單位長度的旋轉向量。

移項得到：

$${d\mathbf e \over d\mathbf \theta} = \mathbf a \times \mathbf r$$


於是我們得到：

$$
\mathbf J_1 =
\frac{\Delta \mathbf e}{\Delta\theta_1}=
\begin{bmatrix}
\frac{\Delta e_{x}}{\Delta\theta_1} \\\\
\frac{\Delta e_{y}}{\Delta\theta_1} \\\\
\frac{\Delta e_{z}}{\Delta\theta_1}
\end{bmatrix}=
\mathbf a_i \times (\mathbf e - \mathbf r_i)
$$

其中 $\mathbf r_i$ 為第 $i$ 個關節的座標向量。

注意到這個算法都是 $\mathbf J_i$ 都是關節的其中 1 維度，所以所有關節加起來如果有 M 個維度，那 $\mathbf J$ 就會是 $3 \times M$ 的矩陣。

實作時，因為 $J_i$ 只有包含 1 維度，所以假設關節 $A$ 可以動的維度有 $(x, z)$，那其角加速度為 $\mathbf \omega_A = (\mathbf\omega_{Ax}, 0, \mathbf\omega_{Az})$。假設 $\mathbf \theta_i$ 代表 $A$ 的 $z$ 軸，那麼 $\mathbf \omega_i$ 為 $\mathbf \omega_{A} \times (0, 0 ,1) = \mathbf\omega_{Az}$。

### 2.5 Inverse of Jacobian

我們為了解 $d\mathbf \theta  = \mathbf J^{-1} d \mathbf e$，已經得到 $\mathbf J$ 之後，我們要算 $\mathbf J^{-1}$，但因為反矩陣必須是方陣，但我們的 $\mathbf J$ 是 $3 \times M$ 的矩陣，所以無法直接取 Inverse，反之我們採用 Pseudo Inverse $\mathbf J^+$。

考慮以下步驟：

$$ d\mathbf e = \mathbf J d\mathbf  \theta$$
$$ \mathbf J^T d\mathbf e = \mathbf J^T J d \mathbf \theta$$
$$ (\mathbf J^T \mathbf J)^{-1} \mathbf J^T d\mathbf e =(\mathbf J^T \mathbf J)^{-1}(\mathbf J^T \mathbf J)d \mathbf \theta$$
$$ (\mathbf J^T \mathbf J)^{-1} \mathbf J^T d\mathbf e =d \mathbf  \theta$$
$$ \mathbf J^+ d\mathbf e =d \mathbf \theta$$
$$ \mathbf J^+ = (\mathbf J^T \mathbf J)^{-1} \mathbf J^T $$


運用 SVD 的性質：

$$SVD(J)=UΣV^∗$$


將剛剛的 $\mathbf J^+$ 代入拆解：

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"> <mtable columnalign="right left right left right left right left right left right left" rowspacing="3pt" columnspacing="0em 2em 0em 2em 0em 2em 0em 2em 0em 2em 0em" displaystyle="true"> <mtr> <mtd> <msup> <mrow class="MJX-TeXAtom-ORD"> <mi mathvariant="bold">J</mi> </mrow> <mo>+</mo> </msup> </mtd> <mtd> <mi></mi> <mo>=</mo> <mo stretchy="false">(</mo> <msup> <mrow class="MJX-TeXAtom-ORD"> <mi mathvariant="bold">J</mi> </mrow> <mo>&#x2217;<!-- ∗ --></mo> </msup> <mrow class="MJX-TeXAtom-ORD"> <mi mathvariant="bold">J</mi> </mrow> <msup> <mo stretchy="false">)</mo> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <msup> <mrow class="MJX-TeXAtom-ORD"> <mi mathvariant="bold">J</mi> </mrow> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> <mtr> <mtd /> <mtd> <mi></mi> <mo>=</mo> <mo stretchy="false">(</mo> <mi>V</mi> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> <mi>U</mi> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>V</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> <msup> <mo stretchy="false">)</mo> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <mi>V</mi> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> <mtr> <mtd /> <mtd> <mi></mi> <mo>=</mo> <mo stretchy="false">(</mo> <mi>V</mi> <msup> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <mn>2</mn> </msup> <msup> <mi>V</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> <msup> <mo stretchy="false">)</mo> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <mi>V</mi> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> <mtr> <mtd /> <mtd> <mi></mi> <mo>=</mo> <mo stretchy="false">(</mo> <msup> <mi>V</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> <msup> <mo stretchy="false">)</mo> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <msup> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>2</mn> </mrow> </msup> <msup> <mi>V</mi> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <mi>V</mi> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> <mtr> <mtd /> <mtd> <mi></mi> <mo>=</mo> <mi>V</mi> <msup> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>2</mn> </mrow> </msup> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> <mtr> <mtd /> <mtd> <mi></mi> <mo>=</mo> <mi>V</mi> <msup> <mi mathvariant="normal">&#x03A3;<!-- Σ --></mi> <mrow class="MJX-TeXAtom-ORD"> <mo>&#x2212;<!-- − --></mo> <mn>1</mn> </mrow> </msup> <msup> <mi>U</mi> <mo>&#x2217;<!-- ∗ --></mo> </msup> </mtd> </mtr> </mtable></math>

### 2.6 IK 演算法

得到 $\mathbf  J+$ 後我們就可以推算上一步的位置：

$$\mathbf \theta_{k} = \mathbf \theta_{k+1} - dt * \mathbf J^+(\mathbf \theta_{k+1}) * d\mathbf e$$

虛擬碼：

```python
while(ABS(current_position - target_position) > epsilon and
      iterator < max_iterator):
    
    1. compute Jacobian J
    2. compute Pseoduinverse Jacobain J^+
    3. compute change in joint DoFs: dθ = (J^+)de
    4. apply the changes to joints. move a small step α: θ += αdθ
    5. update current_position to close target_position
```

## 3. 探討

### 3.1 參數影響

根據公式：
$$\mathbf \theta_{k} = \mathbf \theta_{k+1} - dt * \mathbf J^+(\mathbf \theta_{k+1}) * d\mathbf e$$
每次移動的步數 $dt$ 會影響計算速度，如果每次移動距離太小會導致計算太多次，但如果每次移動距離很大可能會不小心超過目標位置造成難以收斂。

為了避免因為無法收斂，導致迭代太多次，會設定一個誤差值 epsilon，在誤差容忍範圍內停止迭代，同時也會設定一個迭代的上限次數。

IK 事實上不一定有解，目標位置 $t$ 如果超過關節伸展最大長度，或是受限於可轉動的維度，是有機會達不到 $t$。想像一下你的手不管怎樣伸都碰不到天花板，你的手也不可能往外旋轉一直凹，這些情況都屬於無解。實作上也要考慮調整 $t$ 避免成是無解陷入崩潰。

### 3.2 可動關節數量對 IK 的影響

給定一人物，初始狀態如下圖，目標位置為紫色圓點。

![](https://i.imgur.com/Q5zjvcD.png)

Case 1: 設定可以動手臂，以 IK 計算出反推位置：

![](https://i.imgur.com/HTNfgHB.png)
![](https://i.imgur.com/j21wFj9.png)

Case 2: 設定可以動手臂和上半身，以 IK 計算出反推位置：

![](https://i.imgur.com/Lo8DWA3.png)

Case 3: 設定可以動屁股以上，以 IK 計算出反推位置：

![](https://i.imgur.com/KLKFwme.png)

## 4. 結論

透過反向動力法 (IK)，我們得以從人物的原本狀態反推出如何動作達到我們想要的姿勢。對於電腦動畫而言，IK 可以讓動畫人物讓我們設定關鍵影格讓人物做到想要的動作；而對機器人學來說，IK 讓機器手臂可以順利抵達目標作業位置。

IK 有許多種方法，本文只介紹了 Jacobian Pseudoinverse 方法，其特性是會一次更動所有關節，看似會比較真實，但實際上人物動作通常會有比較自然的姿勢，那就要改用會參考真實動作的演算法。根據使用需求可以採用不同演算法，這部分就留給讀者自行研究。

## 5. 參考
- Samuel R. Buss. 2009. Introduction to Inverse Kinematics with Jacobian Transpose, Pseudoinverse and Damped Least Squares methods. [http://graphics.cs.cmu.edu/nsp/course/15-464/Spring11/handouts/iksurvey.pdf](http://graphics.cs.cmu.edu/nsp/course/15-464/Spring11/handouts/iksurvey.pdf)

- [@shi-yan](https://epiphany.pub/@shi-yan). 2019. Inverse Kinematics Explained Interactively. [https://epiphany.pub/@shi-yan/inverse-kinematics-explained-interactively](https://epiphany.pub/@shi-yan/inverse-kinematics-explained-interactively)


- Rickard Nilsson. Inverse Kinematics Explained Interactively. 2009. [https://www.diva-portal.org/smash/get/diva2:1018821/FULLTEXT01.pdf](https://www.diva-portal.org/smash/get/diva2:1018821/FULLTEXT01.pdf)

- [Nancy Pollard](http://www.cs.cmu.edu/~nsp). 2003. CMU: Technical Animation. [http://www.cs.cmu.edu/~15464-s13/assignments/](http://www.cs.cmu.edu/~15464-s13/)
