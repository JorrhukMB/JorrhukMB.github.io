---
layout: post
title:  "AA競程同好會-枚舉"
summary: "參加AA競程同好會學到的一些東西"
author: jorrhukmb
date: '2021-02-05 18:12:00 +0800'
category: notes
thumbnail: /assets/img/posts/Kawaii2.gif
keywords: blog, AA, dreamoon, gray code, brute force
usemathjax: true
permalink: /blog/AA-notes-brute-force/
---

# 枚舉

之前就有稍微學過枚舉，下面是一些我第一次知道的東西

---

## 格雷碼 Gray Code

像下面在利用迴圈進行**狀態壓縮**枚舉的時候，

```cpp
for(int i = 0; i < (1 << n); i++){
	...
}
```

每次會需要再跑一個迴圈去檢查每個位元是否為 **true**，時間複雜度是 $O(2^n\cdot n)$

**格雷碼**是在每次枚舉的時候，只改變其中一個 bit，

---

因此不需要多一個迴圈去判斷，複雜度為 $O(2^n)$


操作很簡單，兩個步驟循環 : 

1. 改變第一個 bit
2. 改變從右數來第一個為 1 的左邊的 bit

舉例 :

```
00
01
11
10
```

---

在 [CSES - Gray Code](https://cses.fi/problemset/task/2205/) 中，為了方便輸出所以使用string去處理

但實際應用的時候總不可能用字串，所以就自己想了一下用位元運算方法

可以利用 **lowbit** 的方法找快速找出第二步要的 bit，然後左移 1 `xor` 一下就好了

```cpp
#define lowbit(x) ((x)&(-x))
void GrayCode(int n){
    int perm = 0;
    for(int i = 0; perm <= (1 << n); i++){
        
        ...

        if(i & 1){
            perm ^= (lowbit(perm)<<1);
        }else perm ^= 1;
    }
}
```

但格雷碼基本上好像不會用到www

直接遞迴枚舉也可以做到同樣的效果

---

## 一個我覺得有趣的東西

在 [AtCoder ABC119 C](https://atcoder.jp/contests/abc119/tasks/abc119_c) 這個問題中，我原本的寫法是做兩次枚舉，

一次枚舉子集，一次枚舉 $N-3$ 個合併操作的方法，雖然 **<span style="color:lightgreen">AC</span>** 了，但我覺得我寫的超醜，所以去看別人怎麼寫的，

[Submission #4369435](https://atcoder.jp/contests/abc119/submissions/4369435) 我看不懂他怎麼寫的就跑去問了電仁，總之我只講一下他的技巧，

以下才是重點ww

他是開 $2N$ 個 bit，用 2 個 bit 去表示一個物品的狀態，超酷ㄉ啦

我之前都沒想過可以不只用 1 個 bit 去**狀態壓縮**

同理也可以用好幾個 bit 去表示一個狀態