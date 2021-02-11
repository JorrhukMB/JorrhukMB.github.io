---
layout: post
title:  "AA競程同好會-數論"
summary: "參加AA競程同好會學到的一些東西"
author: jorrhukmb
date: '2021-02-11 14:24:00 +0800'
category: notes
thumbnail: /assets/img/posts/Kawaii2.gif
keywords: blog, AA, dreamoon, math, fermat, modulo
usemathjax: true
permalink: /blog/AA-notes-math/
---



前幾天在忙寒訓，然後昨天耍廢了一天qq

---

# 數論

大致上就是跟模運算有關

然後數學國手 Arena_Closer 有稍微寫了一些定理的證明 [Several Theorems in Number Theory - HackMD](https://hackmd.io/@701-Coder/N_theorems?fbclid=IwAR11H_XicaXzU4l7yBTL7jAk-O3R9599EccwWgMLKYzjVCQ7mzx1c3XGrc4)

但我看不懂...對

---

##  費馬小定理 Fermat's Theorem

$$
a^{p}\equiv a\pmod p
$$

若 $a,p$ 互質，
$$
a^{p-1}\equiv 1 \pmod p
$$

### 應用

若要計算一個在模運算底下冪次很大的數
$$
a^b \mod p
$$
若 $a,p$ 互質，則相當於
$$
a^{(b\mod p)} \mod p
$$


---

## 模逆元

原理跟證明其實我沒有很清楚，所以下面可能寫得有點隨便



因為除法在取模的時候不能像其他運算一樣簡單

所以就需要模逆元的幫助

假設我們要計算 在$\mod p$ 底下 $x/y$ 的值
$$
{x\over y}\mod p
$$
相當於 $x$ 乘上 $y$ 的反元素(模逆元)
$$
x\cdot y^{-1} \mod p
$$
因此我們需要算出 $y$ 的模逆元

---

模逆元定義如下
$$
a\cdot a^{-1}\equiv1\pmod p
$$
$a^{-1}$ 為 $a$ 的 模逆元

根據 **費馬小定理**，當 $a$、$p$ **互質**時可得
$$
a^{p-1} \equiv 1 \pmod p
$$
結合上面的式子
$$
a\cdot a^{p-2}\equiv1\pmod p
$$
因此模逆元 $a^{-1} \equiv a^{p-2} \pmod p$

再套回第一個式子，
$$
{x\over y}\mod p
=
x\cdot y^{p-2}\mod p
$$
**注意!!**  $a$ 的模逆元存在 若且唯若 $a,p$ 互質