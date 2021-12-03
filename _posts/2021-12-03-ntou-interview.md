---
layout: post
title:  "海大特選面試"
summary: "海洋大學資訊工程學系 特殊選材面試"
author: jorrhukmb
date: '2021-12-03 16:51:00 +0800'
category: interview
thumbnail: /assets/img/posts/ntou.jpg
keywords: interview, college
usemathjax: true
permalink: /blog/ntou-interview/
---

###### 問題統整 : 

1. Deep Learning 運用到甚麼數學

2. 知道範數嗎

3. 學過甚麼程式語言

4. 物件導向是什麼

5. 用迴圈跟遞迴寫  *X~Y所有奇數的和*

6. 哪個執行效率比較好

7. L2 norm 跟向量內積的關係


---

###### 面試

教授B : 請用一分鐘介紹自己有甚麼特殊才能

我 : (略)

教授A : 你剛剛有提到這個Deep Learning，那我你知道Deep Learning有應用到什麼數學?

我 : 有用到微積分，就是訓練的時候會有個Loss Function，他是一個多元的高維的一個曲線，然後我們再用微積分，用偏微分的方式計算梯度，然後往梯度的方向走，就可以找到這個 local minimum 或是 global minimum

教授C : 你知不知道範數

我 : (???) 不，我不知道

教授C : 你學過什麼程式語言

我 : 我學過 C、C++還有一點的 Python

教授C : 那你知道C跟C++的差別在哪裡

我 : C++ 有內建一些的資料結構像是 linked list, stack之類的

教授C : C++ 主要是有物件導向，說一下物件導向是什麼

我 : ( 回答炸了 我又沒學過OOP )

教授C : 好，白板那題用迴圈寫一下

( 題目 : 求 X~Y所有奇數的和 )

我 : 

```cpp
int sum = 0;
for(int i = x; i <= y; i++){
    if(i&1) sum += i;
}
```

教授C : 能再優化嗎

我 : 先判斷x是不是奇數，然後迴圈改成 `i+=2`

教授C : 好，用遞迴寫

我 : (腦袋燒雞 想太複雜 被教授笑了一下)

```cpp
int f(int x, int y){
    if(x == y) return x;
    if(x > y) return 0;
    if(x&1) return x + f(x+2,y);
    else return f(x+1,y);
}
```

教授C : 你這樣 y 不是奇數怎麼辦

我 : (???? 應該沒錯吧  我猜他沒看到我第3行 )

教授C : 好，這樣迴圈跟遞迴哪個效率比較好

我 : 呃 應該是一樣快

( 我當時想說時間複雜度都是O(n)所以一樣，但後來越想越不對勁 )

教授B : 你知道 L2 norm 跟向量的內積有甚麼關係嗎?

我 : (...??)

教授B : 你有想過這個問題嗎?

我 : 沒有

--- 面試結束 ---

---

###### 心得

本來想還原當時的狀況，但太冗長了，最後還是精簡的寫了。

進去前超緊張，但面試過程真的跟聊天沒兩樣，緊張感完全不見。

但出來後我整個大焦慮，很多問題沒有回答好，甚至可能還回答錯的。

希望能正取，讓我增加一點信心。