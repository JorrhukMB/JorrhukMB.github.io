---
layout: post
title:  "擴展歐幾里得算法"
summary: "歐幾里得及其擴展算法筆記"
author: jorrhukmb
date: '2021-02-21 14:17:00 +0800'
category: ['notes','math']
thumbnail: /assets/img/posts/Banner5.gif
keywords: blog, note, math, euclidean, modulo
usemathjax: true
permalink: /blog/euclidean/
---

# 歐幾里得算法

俗稱輾轉相除法

用來求兩數的最大公因數

---

## 算法

$$
\gcd(a,b)=\gcd(a-b, b),\quad a>b\\
\rightarrow\gcd(a,b)=gcd(a\%b, b), \quad a>b
$$

---

## 原理

設
$$
a = 252, b = 105\\
\gcd(a,b)=21\\
252 = 21\cdot12\\
105 = 21\cdot5\\
\because 252-105=21\cdot(12-5)=147\\
\therefore \gcd(105,147) = 21
$$

圖解

![圖 待補]()



# 擴展歐幾里得算法

為歐幾里得算法的擴展 (廢話)

可在利用歐幾里得算法求 $\gcd(a,b)$ 時同時算出一組 $x,y$，使得
$$
ax+by=\gcd(a,b)
$$
也就是滿足[*貝祖等式* ](https://zh.wikipedia.org/wiki/%E8%B2%9D%E7%A5%96%E7%AD%89%E5%BC%8F)(我沒詳細去看是啥)

---

根據歐幾里得算法
$$
\gcd(a,b)=\gcd(a\%b, b),\quad a>b
$$
###### (下面有一部分是抄 wiki 的，因為我不知道要怎麼講得更淺顯易懂)

第 $i$ 步帶餘除法得到的商為 $q_i$，餘數為 $r_{i+1}$，我們可以寫成下面的形式

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/47f5faad419bbd4c3d301d0c74bc1f11196850e8)

當某步得到的 $r_{i+1} = 0$ 時，計算結束，上一步得到的 $r_i$ 即為 $a,b$ 的 $\gcd$

擴展歐幾里得除了 $q_i,r_i$ 外還多紀錄了兩組序列，記作 $s_i, t_i$，使得
$$
a s_i+bt_i=r_i
$$


而透過觀察可發現
$$
a\cdot1+b\cdot0=a\\
a\cdot0+b\cdot1=b
$$
因此
$$
s_0 = 1,\space t_0 = 0\\
s_1 = 0,\space t_1 = 1
$$
而根據 $r_i$ 的遞推式可推得
$$
r_{i+1}\\
= r_{i-1}-q_i r_i\\
= (a s_{i-1}+b t_{i-1}) - q_i(a s_i+b t_i)\\
= (a s_{i-1}-a s_i q_i)+(b t_{i-1}-b t_i q_i)\\
= a(s_{i-1}-s_i q_i)+b(t_{i-1}-t_i q_i)\\
= a s_{i+1} + b t_{i+1}
$$
因此
$$
s_{i+1} = s_{i-1}-s_i q_i\\
t_{i+1} = t_{i-1}-t_i q_i
$$

---

## 應用

---

### 模逆元

假設要求 $a$ 在$ \mod n$ 下的模逆元 $a^{-1}$

利用擴展歐幾里得算法
$$
a x + n y = g
$$
$g$ 為 $\gcd(a,n)$

---

**若 $g = 1$**

$a^{-1}$ 存在
$$
a x + n y = 1\\
\rightarrow a x \equiv 1 \pmod n
$$
即得 $a^{-1} = x$

---

**若 $g \neq 1$**

$a^{-1}$ 不存在
$$
\because a x + n y \neq 1\\
\therefore ax \neq 1 \pmod n
$$

---