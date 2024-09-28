---
title:  "(6) Small Oscillation ─ Example: Sympathetic Vibration"
categories:
  - physics
tags:
  - small_oscillation
---

現在來看一個例子，兩顆粒子串接，中間接一個比較weak的彈簧。

{% include posts-fig.html path="/physics_small_oscillation/Fig12.png" %}



> 這個例子可以用很常見的實驗來做，擺兩張椅子，上面放一根棍子，棍子中間掛兩個一樣的小球，手動讓A小球開始晃，晃著晃著A會越來越慢，然後B會開始晃，過一段時間B會變慢，A再開始晃，稱這個為 Sympathetic Vibration。背後的原因當然是因為中間的棍子再被晃動的時候會有一些力矩，帶動另外一顆再晃，然後維持能量守恆情況下的結果。


## EOM

一樣來寫運動方程式吧！

兩顆粒子

$$
\begin{cases}
m\frac{d^2 x_1}{dt^2}=-Kx_1-C(x_1-x_2)\\
m\frac{d^2 x_2}{dt^2}=-Kx_2-C(x_2-x_1)
\end{cases}\\
(C<<K)
$$

矩陣表示

$$
\begin{pmatrix}
m\omega^2-(K+C) & C\\
C&m\omega^2-(K+C)
\end{pmatrix}
\begin{pmatrix}
x_1\\
x_2
\end{pmatrix}
=\begin{pmatrix}
0\\
0
\end{pmatrix}\\
\Rightarrow m\omega^2-(K+C)=\pm C
$$

求得兩個頻率解和對應的normal modes

$$
\begin{cases}
\omega_1=\sqrt{\frac{K}{m}},\quad\begin{pmatrix}x_1\\x_2\end{pmatrix}\propto\begin{pmatrix}1\\1\end{pmatrix}\\
\omega_2=\sqrt{\frac{K+2C}{m}},\quad\begin{pmatrix}x_1\\x_2\end{pmatrix}\propto\begin{pmatrix}1\\-1\end{pmatrix}
\end{cases}
$$

go on...





