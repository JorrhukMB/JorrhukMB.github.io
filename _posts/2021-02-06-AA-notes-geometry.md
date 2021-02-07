---
layout: post
title:  "AA競程同好會-計算幾何"
summary: "參加AA競程同好會學到的一些東西"
author: jorrhukmb
date: '2021-02-07 16:31:00 +0800'
category: notes
thumbnail: /assets/img/posts/Kawaii2.gif
keywords: blog, AA, dreamoon, geometry, math
usemathjax: true
permalink: /blog/AA-notes-geometry/
---

# 計算幾何

第一次接觸的東西，覺得還蠻有趣的，第一次把高中數學應用在資訊這邊 (排列組合除外。

---

## 向量

基本上就是一堆向量的判斷之類的，先講一下向量的一些基本運算及性質

---

### 向量運算

向量運算有 **向量加減**、**向量乘純量**、**內積**、**外積**

$\vec{a}=(x_1,y_1),\vec{b}=(x_2,y_2)$

- 向量加減 : 

  $\vec{a}+\vec{b}=(x_1+x_2,y_1+y_2)$ 

  $\vec{a}-\vec{b}=\vec{a}+(-\vec{b})=(x_1-x_2,y_1-y_2)$

- 向量乘純量 : 

  $t\cdot\vec{a}=(t\cdot x_1,t\cdot y_1)$

- 向量內積 (Dot product):

  設 $\theta$ 為 $\vec{a},\vec{b}$ 夾角

  $\vec{a}\cdot\vec{b}=\lvert\vec{a}\rvert\lvert\vec{b}\rvert\cdot \cos(\theta)=x_1x_2+y_1y_2$

- 向量外積 (Cross product) : 

  這個108課綱沒教到，所以我沒有到很清楚，以下可能會講錯

  $\vec{a}\times\vec{b}=\lvert\vec{a}\rvert\lvert\vec{b}\rvert\cdot\sin(\theta)=x_1y_2-x_2y_1$

  *幾何意義* : 跟行列式一樣 (還是他們其實是同個東西..?) 可以算出**凸多邊形的面積**

  若 $\vec{a}\times\vec{b}<0$ 則 $\vec{b}$ 在 $\vec{a}$ 的**順**時鐘方向

  若 $\vec{a}\times\vec{b}>0$ 則 $\vec{b}$ 在 $\vec{a}$ 的**逆**時鐘方向

---

### 模板

整數 : 

```cpp
using ll = long long;
struct Point{
    ll x, y;
    Point(ll _x = 0, ll _y = 0) : x(_x), y(_y) {}
    Point operator+(const Point& b)const{return Point(x+b.x, y+b.y);}
    Point operator-(const Point& b)const{return Point(x-b.x, y-b.y);}
    Point operator*(const ll     v)const{return Point( x*v ,  y*v );}
    Point operator/(const ll     v)const{return Point( x/v ,  y/v );}
    ll    operator*(const Point& b)const{return x*b.x + y*b.y; } // Dot Product
    ll    operator/(const Point& b)const{return x*b.y - b.x*y; } // Cross Porduct
    bool operator <(const Point& b)const{
        if(x == b.x) return y < b.y;
        return x < b.x;                                                                                                         
    }
    double dist()const{return sqrt(x*x+y*y);}		// vector magnitude
    double angle()const{return atan2(y,x);}		// direction angle
    friend ostream& operator<<(ostream& os, const Point& a){os<<a.x<<' '<<a.y;}
    friend istream& operator>>(istream& is, Point& a){is>>a.x>>a.y;}
};
```

浮點數 : 

```cpp
const double EPS=1e-12;
const double PI=acos(-1);
struct Point{
    double x,y;
    Point(double _x = 0,double _y = 0): x(_x), y(_y){}
    Point operator+(const Point& b)const{return Point(x+b.x, y+b.y);}
    Point operator-(const Point& b)const{return Point(x-b.x, y-b.y);}
    Point operator*(const double v)const{return Point( x*v ,  y*v );}
    Point operator/(const double v)const{return Point( x/v ,  y/v );}
    double operator*(const Point& b)const{return x*b.x+y*b.y;}
    double operator^(const Point& b)const{return x*b.y-y*b.x;}
    bool operator<(const Point& b)const{
        if(fabs(x-b.x) < EPS){
            if(fabs(y-b.y) < EPS) return 0;
            return y<b.y;
        }
        return x<b.x;
    }
    double dist()const{return sqrt(x*x+y*y);}
    double angle()const{return atan2(y,x);}
    Point rotate(double v)const{return Point(x*cos(v)-y*sin(v),x*sin(v)+y*cos(v));}
    Point unit(){return (*this)/dist();}
    friend ostream& operator<<(ostream& os, const Point& a){os<<a.x<<' '<<a.y;}
    friend istream& operator>>(istream& is, Point& a){is>>a.x>>a.y;}
};
```



---

### 一些我會的計算幾何演算法

---

#### 判斷線段是否相交

[CSES - Line Segment Intersection](https://cses.fi/problemset/task/2190)

問 $\overline{AB}$ 是否與 $\overline{CD}$ 相交

```cpp
int ng(ll x) { if(x < 0) return -1; if(x > 0) return 1; return 0; }
bool inter(Point A, Point B, Point C, Point D){
    if(max(A.x, B.x) < min(C.x, D.x)) return false;
    if(max(C.x, B.x) < min(A.x, B.x)) return false;
    if(max(A.y, B.y) < min(C.y, D.y)) return false;
    if(max(C.y, D.y) < min(A.y, B.y)) return false;
    if(ng((B-A)^(C-A))*ng((B-A)^(D-A)) < 0 && ng((D-C)^(A-C))*ng((D-C)^(B-C)) < 0) return true;
    return false;
}
```

因為可能會爆 long long ，所以加了 ng$()$ 去處理

前面 4 個是先把 $\overline{AB}$ 跟 $\overline{CD}$ 的 $x$ 軸、 $y$ 軸完全相離的情況先特判掉

之後就是用外積的方式判斷 $\vec{AB}$ 與 $C、D$ 以及 $\vec{CD}$ 與 $A、B$ 的外積是否為負，也就是分別在線段的兩邊

---

#### 判斷一點是否在線段上

問 $C$ 是否在 $\overline{AB}$ 上

```cpp
bool on_side(Point C, Point A, Point B){
	if((A-C)*(B-C) < 0 && (A-C)^(B-C) == 0) return true;
    return false;
}
```

先內積判斷 $\overline{CA}、\overline{CB}$ 夾角 $>90^{\circ}$，之後再外積判斷 $\overline{CA}、\overline{CB}$ 平行。

---

#### 點與凸多邊形關係

[CSES - Point in Polygon](https://cses.fi/problemset/task/2192)

問 $A$ 是在凸多邊形的裡面、外面還是邊界上

先把在邊界上的情形特判掉後

從 $A$ 延伸一條無限長的向量 $\vec{AB}$，分兩種情況討論

- $\vec{AB}$ 與凸多邊形交點個數為**奇數** $\Rightarrow$ 裡面
- $\vec{AB}$ 與凸多邊形交點個數為**偶數** $\Rightarrow$ 外面

但延伸的 $\vec{AB}$ 有可能會跟凸多邊形的頂點相交，這樣就會爛掉

但若凸多邊形的頂點都在整數點上，那麼只要把 $\vec{AB}$ 設為 $(x_A+\infty, y_A+1)$就不會發生這種情況了

---

#### 凸包

[CSES - Convex Hull](https://cses.fi/problemset/task/2195)

我會的演算法 : Andrew's Monotone Chain [演算法筆記](http://web.ntnu.edu.tw/~algo/ConvexHull.html#4)

就是一直維護 $\vec{s[i-2]s[i-1]}\times\vec{s[i-2]s[i] > 0}$