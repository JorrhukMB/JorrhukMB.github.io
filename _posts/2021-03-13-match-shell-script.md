---
layout: post
title:  "Linux對拍shell script"
summary: "如題"
author: jorrhukmb
date: '2021-03-13 11:50:00 +0800'
category: ['notes','debug']
thumbnail: /assets/img/posts/Banner5.gif
keywords: blog, note, linux, math, script, debug
usemathjax: true
permalink: /blog/match-script/
---

天啊好久沒碰競程了，開學後能練的時間變得超少，最近總算有時間可以練了@@

TOI 的心得文等我心血來潮的時候再寫吧ww

回歸主題

---

# 對拍

**對拍**是一種debug的方法，用來找會讓你程式 WA 的測資

直接用 shell script 來解釋

```bash
#!/bin/bash
while true; do
	./r > input
	./a < input > output.a
	./b < input > output.b
	diff output.a output.b
	if [ $? -ne 0 ] ; then break; fi
done
```

`./r` 是生成隨機測資的程式

`./a` 是輸出正確的code

`./b` 是找不到bug的code

之後比較 `output.a`, `output.b` 不一樣的就break

---

使用的時機像是

- `./a` 是確認輸出會對 但會TLE，`./b` 找不到 bug