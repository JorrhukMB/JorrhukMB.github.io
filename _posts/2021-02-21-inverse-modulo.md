---
layout: post
title:  "模逆元算法統整"
summary: "如題"
author: jorrhukmb
date: '2021-02-21 15:08:00 +0800'
category: ['notes','math', 'modulo']
thumbnail: /assets/img/posts/Banner5.gif
keywords: blog, note, math, euclidean, modulo, fermat
usemathjax: true
permalink: /blog/inverse-modulo/
---

---



###### Edited : 2021/03/01

Added Euler's Theorem



---

#  模逆元

$$
a\cdot a^{-1} \equiv 1 \pmod n
$$

下面是幾種計算模逆元的方法

---

## 費馬小定理

詳細 : [AA競程同好會-數論](https://jorrhukmb.github.io/blog/AA-notes-math/)



$$
a^{-1} = a^{n-2}
$$



**若且唯若** $n$ **為質數**

否則請用下面的歐拉定理

---

## 歐拉定理

詳細 : [Euler's Totient Function/Theorem](/blog/Euler)


$$
a^{-1} = a^{\varphi(n)-1}
$$


**若且唯若** $\gcd(a,n)=1$

否則 $a^{-1}$ 不存在

---

## 擴展歐幾里得

詳細 : [擴展歐幾里得算法](https://jorrhukmb.github.io/blog/euclidean/)

利用擴展歐幾里得算法求出一組不定方程解



$$
ax + ny = g
$$



$g = \gcd(a,n)$

**$a^{-1} = x$ 若且唯若 $g = 1$**

否則 $a^{-1}$ 不存在 

---

