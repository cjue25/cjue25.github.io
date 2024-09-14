---
title:  "(2) Small Oscillation ─ Periodic Boundary Condition & Example"
categories:
  - physics
tags:
  - small_oscillation
---

## 求解N顆粒子的Normal Modes

現在來舉個簡單的粒子，假設一條彈簧，兩邊接牆壁，中間串N顆粒子，求解EOM。

{% include posts-fig.html path="/physics_small_oscillation/Fig2.png" %}


對於$j^{th}$粒子，EOM

$$
m\frac{d^2\delta R_j}{dt^2} = -k(\delta R_j - \delta R_{j+1}) -k(\delta R_j - \delta R_{j-1})\\
= -2k \delta R_j + k(\delta R_j + \delta R_{j+1})\\
(j=1,2,\cdots,N)
$$

邊界條件BC為

$$
\begin{cases}
\delta R_0 = 0\\
\delta R_{N+1} = 0
\end{cases}
$$


根據上一節的討論，求該粒子的Normal Mode

$$
-\omega^2 m \delta R_j = -2k \delta R_j + k(\delta R_{j-1} + \delta R_{j+1})
$$


### 方法一


我們試著直覺地一步一步拆解，先隨便猜一個$\omega$代進去。


#### (1) $j=1$

對$j=1$來說

$$
-\omega^2 m \delta R_1 = -2k \delta R_1 + k(\underbrace{\delta R_0}_{0} + \delta R_2)
$$


可以看到我們可以用$\delta R_1$來表示$\delta R_2$。

#### (2) $j=2$

同理對$j=2$

$$
-\omega^2 m \delta R_2 = -2k \delta R_2 + k(\delta R_1 + \delta R_3)
$$

因為$\delta R_2$可以用$\delta R_1$表示，那這裡待求的$\delta R_3$一樣可以用$\delta R_1$來替換。

#### (3) $j=N$

重複上述步驟一直求

$$
\delta R_1, \delta R_2, \cdots, \delta R_N
$$

並且都用$\delta R_1$來替換(公式會超複雜)。


不過回來看一下最後一顆的公式，求$N^{th}$粒子時，會算$\delta R_{N+1}$

$$
-\omega^2 m \delta R_N = -2k \delta R_N + k({\delta R_{N-1}} + \underbrace{\delta R_{N+1}}_{?})
$$


#### (4) 邊界條件的問題？



我們從前面的邊界條件知道$\delta R_{N+1}$要等於0，但一開始我們是隨便猜$\omega$的數值，可能解到第N步發現$\delta R_{N+1}$不等於0，那就代表猜錯了，要再重新用別$\omega$！



需要猜到真正對的$\omega$，才能最後滿足邊界條件$\delta R_{N+1}=0$，這也是為什麼求 Normal Modes 頻率一定是特定值的關係。


從這裡可以更清楚地看到，完全符合我們以前所學的，像是多加了邊界條件之後，解會量子化的關係等等，因為這些邊界條件導致$\omega$一定是特定的數值，不能是任意的。


可是，那我們怎麼知道一開始到底要怎麼猜！？



所以這個方法一定是不可行！


### 方法二

我們換個進階的方法。


把原本的 3-terms recursion relation

$$
-m\omega^2 \delta R_j = -2k \delta R_j + k(\delta R_{j-1} + \delta R_{j+1})
$$

改寫一下

$$
\Rightarrow \left(\frac{-m\omega^2}{k}+2\right)\delta R_j - \delta R_{j-1} =\delta R_{j+1}
$$

再轉換成矩陣模式 2-term recursion relation

$$
\Rightarrow \begin{pmatrix} \delta R_{j+1} \\ \delta R_j \end{pmatrix} = \begin{pmatrix} -\frac{m\omega^2}{k}+2 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} \delta R_j \\ \delta R_{j-1} \end{pmatrix}\\
\Rightarrow \vec{W}_{j+1} = \hat{A} \vec{W}_j
$$


展開求到N+1項

$$
\Rightarrow \vec{W}_{N+1} = \hat{A} \vec{W}_N = \hat{A}^2 \vec{W}_{N-1} = \cdots = \hat{A}^N \vec{W}_1
$$


這時重點就在於要求解

$$
\hat{A}^N
$$

簡單一點就是去算對角化的矩陣 (2D eigen problem)

$$
\begin{cases}
\hat{A} \vec{\epsilon}_1 = \Lambda_1 \vec{\epsilon}_1\\
\hat{A} \vec{\epsilon}_2 = \Lambda_2 \vec{\epsilon}_2\\
\end{cases}
$$

$$
\vec{\epsilon}_j\in\mathbb{R}^2
$$

並且寫下初始值

$$
\vec{W}_1 \equiv l_1\vec{\epsilon}_1 + l_2\vec{\epsilon}_2\\
(l_1, l_2\text{ numerical value})
$$

合併一下

$$
\begin{align}
\Rightarrow \hat{A}^N \vec{W}_1 &= \Lambda_1^N l_1 \vec{\epsilon}_1 + \Lambda_2^N l_2 \vec{\epsilon}_2\\
&=\vec{W}_{N+1}\\
&\equiv\begin{pmatrix} \delta R_{N+1} \\ \delta R_N \end{pmatrix}\\
\end{align}
$$

#### 邊界條件仍然是問題

看起來公式簡單多了，可是為了要符合邊界條件的$\delta R_{N+1}=0$，**我們還是得去猜$\omega_1$**，即便狂調整到對了，但一樣也只能解這次的問題。


如果下一個問題碰到$k$不一樣，或是邊界條件有點小變，或是中間有一顆粒子沒串，那整個就還是得重新猜重新解！


### 方法三：Periodic Boundary Condition

這時候我們從物理的自然現實出發，雖然自然頻率會和邊界條件有關係，但我們預期像是一塊晶體，一個金條，很長很大，假設有一億顆在裡面，那即便稍微改一點邊界條件，數學上的確自然頻率會變，但會覺得這些遠遠的變動改變不大，**物理上對自然頻率不會改變太多**。


想像上就是把剛剛一串的彈簧頭尾給接起來！稱為 Periodic Boundary Condition，如下圖


{% include posts-fig.html path="/physics_small_oscillation/Fig3.png" %}


不過還是說明一下，其實也不是說物理上這樣做就是對的，這個「可連」的重點在於系統有**對稱性(translational symmetry)**，整個系統移一點點還是一樣的symmetry，所以物理上相信真實的系統，因為粒子很多(N很大)，所以邊邊改變一點，對中間的影響不大，算是一種犧牲Boundary Condition，但是解法就變得很簡單。

## 舉例

現在我們就結合方法二和方法三繼續解下去。

### Translational Symmetry Operator

前面說到，用到 periodic boundary condition 隱含著 translation symmetry，所以如果


$$
\begin{pmatrix} \delta R_{1} \\ \delta R_2 \\ \delta R_3 \\ \vdots \\ \delta R_N \end{pmatrix}
$$

是解答，那麼我們定一個translational symmetry operator

$$
\hat{P}
$$

使得

$$
\hat{P}(\delta \vec{R})\equiv \begin{pmatrix}  \delta R_2 \\ \delta R_3 \\ \vdots \\ \delta R_N \\ \delta R_{1} \end{pmatrix}
$$

也會是解答。


如果我們重複做N次，就會回到原本自己，所以

$$
\hat{P}^N=\hat{\mathbb{1}}
$$

#### Eigenvalue

若

$$
\hat{P}^N=\hat{\mathbb{1}}
$$

要求其的Eigenvalue $\lambda$，則可知

$$
\lambda^N = 1
$$

複數解可得(這裡簡單點處理N是偶數的情況)

$$
\lambda_l = e^{i\frac{2\pi l }{N}},\quad l=-\frac{N}{2}, -\frac{N}{2}+1, ..., \frac{N}{2}-1, \frac{N}{2}\\
\left((e^{i\theta})^N=1, \quad \theta=\frac{2\pi}{N}\cdot l\right)
$$

#### Eigenvector

線性代數知道，若兩個operator commute，則有相同的eigen vector。


因此這裡因為$[\hat{P}, \hat{c}]=0$，所以前一節算的normal modes就是$\hat{P}$的 eigen vector。

$$
\hat{P}\begin{pmatrix} \delta R_{1} \\ \delta R_2 \\ \delta R_3 \\ \vdots \\ \delta R_N \end{pmatrix}
\equiv\begin{pmatrix}  \delta R_2 \\ \delta R_3 \\ \vdots \\ \delta R_N \\\delta R_{1} \end{pmatrix}
=e^{i\frac{2\pi}{N}l}\begin{pmatrix} \delta R_{1} \\ \delta R_2 \\ \delta R_3 \\ \vdots \\ \delta R_N \end{pmatrix}
$$

展開條列一下

$$
\begin{align}
\delta R_2 &= e^{i\frac{2\pi}{N}l}\delta R_1\\
\delta R_3 &= e^{i\frac{2\pi}{N}l}\delta R_2 = e^{(i\frac{2\pi}{N}l)\times 2}\delta R_1 \\
&\vdots\\
\delta R_j &= e^{(i\frac{2\pi}{N}l)(j-1)}\delta R_1\equiv e^{(i\frac{2\pi}{N}l)(j)}\delta R_0\\
&(j\text{: index of the }j^{th}\text{ particle})
\end{align}
$$

### 波的形式

前面我們都指定是哪一顆粒子，現在更general一點，直接定位置

$$
x\equiv j\cdot a
$$

其中$a$是每一個粒子之間的距離(lattice spacing)。


所以

$$
\delta R_j = e^{(i\frac{2\pi}{N}l)(j)}\delta R_0\\
\Rightarrow \delta R_x = e^{i\frac{2\pi l}{Na}ja}\delta R_0\equiv e^{ik_l x}\delta R_0\\
k_l\equiv \frac{2\pi}{Na}l\\
(\text{a sort of wave number indexed by }l)
$$

這裡解釋一下，當初我們在解eigenvalue和eigenvector的時候，是用$l$來代表，所以現在定義的$k_l$就是把該組eigenvector(eigenvalue)轉成**波**的形式，$k_l$就是wave number。


而每組eigenvetor，就是這串上所有粒子的displacement($\delta R_x)$，所以簡單來說，每一組eigenvector展現的粒子displacement(normal modes)，都對應到一個波數為$k_l$的波。


反過來說，假設有一百顆粒子，就有一百個normal modes，每一個normal mode的wave number對應的波動，就是這一百個粒子在當下的displacement。


因此我們可以進一步去寫

$$
\delta R_x\propto e^{ik_l x}e^{-i\omega_l t}
$$

這裡的$\omega_l$也用$l$當作label，因為代表normal frequency也是對照到每一組eigenvector。


那麼這個式子整合起來就是個**propagating wave pattern**(往左往右)的plane wave了！

#### 短波長波

$l$竟然決定了是哪一個normal modes，那我們來看極端的情況。


因為

$$
\delta R_j = e^{(i\frac{2\pi l}{N})}\delta R_{j-1}
$$


若 $l=N/2$，$e^{i\pi}=-1$，代表每個相鄰的粒子都是180度的out of phase，排列就很像是↑↓↑↓，直接顛倒運動，波長是最短的。


相反若 $l$ 很小，那鄰居就都差一點，變化很緩慢，看起來就是比較平緩的波，就會是長波。


### 求解EOM

講了一堆，直接回來EOM求解。記得一開始(這裡以防跟波數混淆，彈性係數用C取代)

$$
m\frac{d^2\delta R_j}{dt^2} = -C(\delta R_j - \delta R_{j+1}) -C(\delta R_j - \delta R_{j-1})\\
\Rightarrow -m\omega^2\delta R_j = -C(\delta R_j - \delta R_{j+1}) -C(\delta R_j - \delta R_{j-1})
$$

又

$$
\because \delta R_j \propto e^{i\frac{2\pi l}{N}\cdot j}
$$

我們再把$\delta R_j \equiv 1$簡單化代進去

$$
\begin{align}
\Rightarrow -m\omega^2_l\cdot 1 &= -2C\cdot 1 + C e^{-i\frac{2\pi l}{N}(-1)}+Ce^{i\frac{2\pi l}{N}}(1)\\
-m\omega^2_l\cdot 1 &= -2C\cdot 1 + 2C \cos{\frac{2\pi l}{N}}
\end{align}
$$

移項

$$
\begin{align}
\omega_l^2&=\frac{2C}{m}\left(1-\cos{\frac{2\pi l}{N}}\right)=\frac{2C}{m}2\bigg|\sin{\frac{2\pi l}{N}}\bigg|\\
\Rightarrow \omega_l&=\sqrt{\frac{C}{m}}2\bigg|\sin{\frac{\pi l}{N}}\bigg|=\sqrt{\frac{C}{m}}2 \sin{\frac{ka}{2}}\\
\end{align}
$$

可以看到

$$
\omega=\omega(k)
$$

$\omega$和$k$非線性關係，是dipersive wave！


#### Dispersive Wave

不過我們可以畫個圖來分析一下

{% include posts-fig.html path="/physics_small_oscillation/Fig4.png" %}

- 若$k$很小：可以視為線性沒有dipersive

$$
\omega_k=\sqrt{\frac{C}{m}}2\frac{ka}{2}=\left(\sqrt{\frac{C}{m}}a\right)k\\
\text{No diespersion wave speed: }\frac{\omega_l}{k}=\sqrt{\frac{C}{m}}a
$$

- $k$越大：dispersion就看得出來，$\omega$對應的點就不是等間隔了(有疏密的變化)！


<div class="post_note">
Note:
<br>
The distribution of the normal modes is uniform in $k$, but not in $\omega$！
</div>
