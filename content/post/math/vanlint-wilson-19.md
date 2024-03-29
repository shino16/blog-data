---
title: "Vanlint Wilson 19"
date: 2020-10-30T14:25:20+09:00
draft: true
hidden: true
tags:
- 数学
---

※※　注意　誤植が大量に含まれている可能性があります　※※

<!-- ### ラグランジュの四平方定理

任意の自然数は $4$ つの平方数の和で表される。（証明略）

### 補題

整数 $a_1,a_2,a_3,a_4,x_1,x_2,x_3,x_4$ について、

$$ (a_1^2 + a_2^2 + a_3^2 + a_4^2)(x_1^2 + x_2^2 + x_3^2 + x_4^2) = (y_1^2  + y_2^2 + y_3^2 + y_4^2) $$

を満たす整数 $y_1, y_2, y_3, y_4$ が存在する。

**証明** 行列 $\bm{H}$ を

$$ \bm{H} = \begin{pmatrix}
      a_1 & a_2 & a_3 & a_4 \\\\ 
      -a_2 & a_1 & -a_4 & a_3 \\\\ 
      -a_3 & a_4 & a_1 & -a_2 \\\\ 
      -a_4 & -a_3 & a_2 & a_1
    \end{pmatrix}
$$

とおくと、$\bm{H}\bm{H}^\top = (a_1^2 + a_2^2 + a_3^3 + a_4^4)I$

そこで、$\bm{x} = (x_1,x_2,x_3,x_4), \bm{y} = (y_1,y_2,y_3,y_4)$ とし、$\bm{y} = \bm{x}\bm{H}$ とすると、

$$ \begin{aligned}
  \bm{y}\bm{y}^\top &= y_1^2  + y_2^2 + y_3^2 + y_4^2 \\\\ 
  \bm{x}\bm{H}(\bm{x}\bm{H})^\top &= \bm{x}(\bm{H}\bm{H}^\top)\bm{x}^\top \\\\ 
    &= (a_1^2 + a_2^2 + a_3^2 + a_4^2)(x_1^2 + x_2^2 + x_3^2 + x_4^2)
\end{aligned} $$

より示された。

## 定理 19.11

$v, k, \lambda$ が $\lambda(v-1) = k(k-1)$ を満たす整数であるとき、対称 $2-(v,k,\lambda)$ デザインが存在するには次が必要である。

1. $v$ が偶数ならば、$k-\lambda$ は平方数
2. $v$ が奇数ならば、$(x,y,z) \neq (0,0,0)$ かつ $z^2 = (k-\lambda)x^2+(-1)^{(v-1)/2}\lambda y^2$ であるような整数 $x, y, z$ が存在する。

**証明** 1. は定理 19.7 で示されている。以下 $v$ が奇数の場合を示す。

ある $2-(v,k,\lambda)$ デザインについて結合行列を $N = (n_1,\ldots,n_v)^\top$ とし、$n = k-\lambda$ とおく。また、$\bm{x}=(x_1,\ldots,x_v)^\top$ の多項式 $\bm{L}=(L_1,\ldots,L_v)^\top$ を

$$ L_i = \sum_{j=1}^v n_{ij}x_j $$

とおく。定理 19.9 から $N^\top N = (k-\lambda)I+\lambda J$ なので、

$$ \bm{x}^\top(N^\top N)\bm{x} = n\bm{x}^\top I\bm{x} + \lambda \bm{x}^\top J\bm{x} $$

ここで

$$ (\text{左辺}) = (N\bm{x})^\top N\bm{x} = \bm{L}^\top \bm{L} = L_1^2 + \cdots + L_v^2 $$
$$ (\text{右辺}) = n(x_1^2 + \cdots + x_v^2) + \lambda(x_1 + \cdots + x_v)^2 $$
$$ \therefore\quad L_1^2 + \cdots + L_v^2 = n(x_1^2 + \cdots + x_v^2) + \lambda(x_1 + \cdots + x_v)^2 \quad (*) $$

ラグランジュの四平方定理と補題から、次を満たす $y_1, y_2,\ldots$ をとれる。

$$ n(x_i^2 + x_{i+1}^2 + x_{i+2}^2 + x_{i+3}^2) = y_i^2 + y_{i+1}^2 + y_{i+2}^2 + y_{i+3}^2 \quad (i=1,5,9,\ldots) $$

補題の証明中の $\bm{H}$ が可逆であることから、各 $x_i$ を（ゆえに各 $L_i$ も）$y_i$ の $\mathbb{Q}$ 係数線型結合で表せることに注意。

#### $v \equiv 1 \pmod 4$ の場合

$$ (*) \quad L_1^2 + \cdots + L_v^2 = y_1^2 + \cdots + y_{v-1}^2 + nx_v^2 + \lambda w^2 $$

と書ける。ただし $L_1,\ldots,L_v,w$ は $y_1,\ldots,y_{v-1},x_v$ の線型結合。

$x_1,\ldots,x_v$ のかわりに $y_1,\ldots,y_{v-1},x_v$ の値をそれぞれ選んでよいので、$L_1 = y_1$ または $L_1 = -y_1$（$y_1$ の項が打ち消されない方）とおく。

これを $y_1$ について解き（$y_2,\ldots,y_{v-1},x_v$ の $\mathbb{Q}$ 係数線型結合となる）、$L_2,\ldots,L_v,w$ 中の $y_1$ を置き換えることで、次に帰着する。

$$ L_2^2 + \cdots + L_v^2 = y_2^2 + \cdots + y_{v-1}^2 + nx_v^2 + \lambda w^2 $$

これを繰り返し、$L_v^2 = nx_v^2 + \lambda w^2$ を得る。$x_v \in \mathbb{Q}$ の値を任意にとると $y_{v-1},\ldots,y_1,w,L_v^2 \in \mathbb{Q}$ の値が定まり、分母を払って主張を得る。

#### $v \equiv 3 \pmod 4$ の場合

$(*)$ の両辺に $nx_{v+1}^2$ を足して、

$$ (*) \quad L_1^2 + \cdots + L_v^2 + nx_{v+1}^2 = y_1^2 + \cdots + y_{v+1}^2 + \lambda w^2 $$

これは先ほどと同様の手順により $nx_{v+1}^2 = y_{v+1}^2 + \lambda w^2$ に帰着し、分母を払って主張を得る。 -->

## 復習

デザイン $t$-$(v,k,\lambda)$、$S_\lambda(t,k,v)$：点が $v$ 個、ブロック（ここでは点集合の部分集合）のサイズが $k$、$t$ 個の相異なる点を選ぶとそれらすべてと接続するブロックがちょうど $\lambda$ 個存在する

定理19.11：$2$-$(v,k,\lambda)$ デザインの存在には次が必要：

1. $v$ が偶数のとき $k-\lambda$ は平方数
2. $v$ が奇数のとき方程式 $z^2=(k-\lambda)x^2+(-1)^{(v-1)/2}\lambda y^2$ は非自明な整数解をもつ

## 例19.10

定理19.11 を使ってみましょう

#### 位数 $n = 6$ の射影平面（$\lambda=1$ の symmetric design）

※ $n=2,3,4,5,7,8,9$ の場合は $F_n$ を使って $PG_2(n)$ が構成できる

※ $v = n^2+n+1, k=n+1, \lambda=1$ $\quad \therefore \ \lambda(v-1)=k(k-1)=n^2+n$

$v$ は奇数より、$z^2 = (k-\lambda)x^2 + (-1)^{(v-1)/2}\lambda y^2$（すなわち $z^2 = 6x^2 - y^2$) を満たす非零の整数解の存在が必要。

そのような解が存在すると仮定する。一般性を失わず $\gcd(x,y,z)=1$ を仮定する（$x,y,z$ をそれぞれ $\gcd(x,y,z)$ で割ったものを考える）。

$y,z$: 奇数 より $y^2 \equiv z^2 \equiv 1 \pmod 8$。$6x^2 \equiv 0,6 \pmod 8$ より矛盾。

※ $n^2 \equiv 0,1 \pmod 8$、$n$ が奇数なら $n^2 \equiv 1 \pmod 8$、下図参照

|$n$|0|1|2|3|4|5|6|7|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|$n^2 \bmod 8$|0|1|4|1|0|1|4|1|

#### 位数 $10$ の射影平面

$z^2 = 10x^2 - y^2$ は解 $(x,y,z) = (1,1,3)$ を持つため、定理19.11は使えない。

位数 $10$ の射影平面が存在しないことが1989年にコンピュータによる探索で示された（定理19.11以外の方法で非存在が示された唯一の例）。

## 系

位数 $n \equiv 1, 2 \pmod 4$ の射影平面が存在するならば、$n$ は $2$ つの平方数の和である。

#### 証明

$n \equiv 1, 2 \pmod 4$ より $v = n^2 + n + 1 \equiv 3 \pmod 4$、定理19.11よりある非零の整数 $x,y,z$ が存在して $nx^2 = y^2 + z^2$。

ここで、任意の正整数 $n$ について「$n$ が $2$ つの平方数の和 $\Longleftrightarrow$ 任意の素数 $p \equiv 3 \pmod 4$ は $n$ をちょうど偶数回割り切る」（後述）を使うと、$nx^2$ が後者の条件を満たすことから $n$ も $2$ つの平方数であるといえる。

### 補題

<!--
奇素数 $p$ について、$p$ が $2$ つの平方数の和で表される $\Longleftrightarrow$ $p \not\equiv 3 \pmod 4$

#### 証明

$(\Longrightarrow)$ 平方数は $0, 1 \pmod 4$ なので明らか。

$(\Longleftarriw)$ $p=2$ のとき $p = 1^2 + 1^2$ より明らか。以下 $p \equiv 1 \pmod 4$ と仮定する。

$r^2 \equiv -1 \pmod p$ を満たす $r$ をとる（注）。$0 \leq x_i, y_i < \sqrt{p}$ を満たす組 $(x_i, y_i)$ の数は $(\lfloor \sqrt{p} \rfloor} + 1)^2 > p$。よって鳩ノ巣原理より $(x_i, y_i) \neq (x_j, y_j)$ かつ $x_i-ry_i \equiv x_j-ry_j \pmod p$ を満たすものがとれる。

$x = |x_i-x_j|$、$y = |y\lambda\dbignom{v-1}{t-1}/\dbinom{k-1}{t-1} = _i-y_j|$ とおくと $x^2 \equiv r^2y^2 \equiv -y^2 \pmod p$、よって $x^2 + y^2 \equiv 0 \pmod p$。$x, y < \sqrt{p}$ より $0 < x^2 + y^2 < p$ から $x^2 + y^2 = p$。

（注）平方剰余の相互法則 第一補充法則

$r = (\frac{p-1}{2})!$ とおくと、$$\begin{aligned}(p-1)! &\equiv (\frac{-p+1}{2})(\frac{-p+3}{2})\cdots(-1)(1)\cdots(\frac{p-1}{2}) \\\\ &\equiv (-1)^{\frac{p-1}{2}}r^2 \pmod p \end{aligned}$$

$p \equiv 1 \pmod 4$ のとき $frac{p-1}{2}$ は偶数であり、$(p-1)! \equiv -1 \pmod p$（ウィルソンの定理）であるから $r^2 \equiv -1 \pmod p$

### 補題

任意の正整数 $n$ について、$n$ が $2$ つの平方数の和 $\Longleftrightarrow$ 任意の素数 $p \equiv 3 \pmod 4$ は $n$ をちょうど偶数回割り切る

#### 証明

$(\Longleftarrow)$ $n$ が $2$ つの平方数の和で表される数の積であるとき、$(a^2+b^2)(c^2+d^2) = (ac-bd)^2+(ad+bc)^2$ より$n$ も $2$ つの平方数の和で表される。

$(\Longrightarrow)$  -->

**ガウス整数環** $\mathbb{Z}[i] = \\{a + bi \mid a, b \in \mathbb{Z}\\}$ を用いる。

* $\mathbb{Z}[i]$ は**整域**（非零元の積が非零である、$\\{0\\}$でない可換環）

* **ノルム** $$N(a+bi) = a^2 + b^2 \quad (= |a+bi|^2)$$

  ※ $N(z) = z\overline{z}$、$N(z)N(w) = N(zw)$

* **ユークリッド除法** 任意の $a,b \in \mathbb{Z}[i]$ $(b \neq 0)$ について、$a = bq+r$ かつ $N(r) < N(b)$ を満たす $q,r \in \mathbb{Z}[i]$ が存在する。

  ※ $\dfrac{a}{b}$ に最も近いガウス整数を $q$ とおくと、$$\left|\frac{a}{b}-q\right| \leq \frac{1}{\sqrt{2}}$$ より $$N(r) = N(a-bq) = N(b)N\left(\frac{a}{b}-q\right) \leq \frac{N(b)}{2}$$

これらを使って**ガウス素数**や**素因数分解の一意性**といった概念が成立する。（ガウス整数環はユークリッド環であるので一意分解環）

$p \neq \pm 1, \pm i$ がガウス素数であるとは、$p$ が自明な約数（ノルムが $1, p^2$）以外の約数を持たないことをいう。

（注意）$\mathbb{Z}$ における素数が $\mathbb{Z}[i]$ においてもガウス素数であるとは限らない。<br>
例：$2=(1+i)(1-i),5=(2+i)(2-i)$

#### 補題

素数 $p \equiv 3 \pmod 4$ はガウス素数である。

**証明** $p$ が非自明な約数 $a + bi$ を持つとき $N(a+bi) \mid N(p) = p^2$ であるが、$a^2+b^2 = p$ と仮定すると $p \equiv 3 \pmod 4$ に矛盾。

#### 補題

素数 $p \equiv 3 \pmod 4$ が $a^2 + b^2$ を割り切るとき、$p \mid a$ かつ $p \mid b$。

**証明** $p \mid (a+bi)(a-bi)$。$p$ はガウス素数なので $p \mid a+bi$ または $p \mid a-bi$。

#### 補題 $(\Longrightarrow)$

任意の正整数 $n$ について、$n$ が $2$ つの平方数の和ならば、任意の素数 $p \equiv 3 \pmod 4$ は $n$ をちょうど偶数回割り切る。

**証明** 帰納的に示す。$n = 1$ のとき明らか。$1, \ldots, n-1$ について示されており、素数 $p \equiv 3 \pmod 4$ について $p \mid n = a^2 + b^2$ であるとき、$p \mid a$、$p \mid b$ より $p^2 \mid n$ であり、$n/p^2$ の場合に帰着される。

#### 補題（平方剰余の相互法則 第一補充法則）

$p \equiv 1 \pmod 4$ のとき、ある $x \in \mathbb{Z}/p\mathbb{Z}$ が存在して $x^2 \equiv -1 \pmod p$。

**証明** $x = (\frac{p-1}{2})!$ とおくと、$$\begin{aligned}(p-1)! &\equiv (\frac{-p+1}{2})(\frac{-p+3}{2})\cdots(-1)(1)\cdots(\frac{p-1}{2}) \\\\ &\equiv (-1)^{(p-1)/2}x^2 \pmod p \end{aligned}$$

$\frac{p-1}{2}$ は偶数であり、$(p-1)! \equiv -1 \pmod p$（ウィルソンの定理）であるから $x^2 \equiv -1 \pmod p$
<!-- 
※ オイラーの規準を使えばすぐ

$$ \left(\dfrac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod p $$ -->

#### 補題

素数 $p \not\equiv 3 \pmod 4$ はガウス素数ではない。

**証明** $p = 2$ の場合は $2 = (1+i)(1-i)$ より明らか。

$p \equiv 1 \pmod 4$ がガウス素数と仮定する。ある $x$ が存在して $p \mid x^2+1 = (x+i)(x-i)$ より $p \mid x+i$ または $p \mid x-i$ だが、どちらも成り立たず矛盾。

#### 補題（フェルマーの二平方定理）

素数 $p \not\equiv 3 \pmod 4$ は $2$ つの平方数の和である。

**証明** 非自明な $p$ の約数 $a+bi$ について $N(a+bi) = a^2 + b^2 = p$。

#### 補題

$n, m$ が $2$ つの平方数の和ならば、$nm$ も $2$ つの平方数の和である。

**証明** $n = a^2+b^2$、$m = c^2 + d^2$ とおく。

$$ nm = (a^2+b^2)(c^2+d^2) = (ac-bd)^2+(ad+bc)^2 $$

※ ブラーマグプタ-フィボナッチ恒等式と呼ばれる。$N(a+bi)N(c+di) = N((a+bi)(c+di))$ とも説明できる。

#### 補題 $(\Longleftarrow)$

任意の正整数 $n$ について、任意の素数 $p \equiv 3 \pmod 4$ が $n$ をちょうど偶数回割り切るならば、$n$ は $2$ つの平方数の和である。

　

---

　

## 問題 19L

対称 $2-(29, 8, 2)$ デザインは存在しない。

#### 証明

$\lambda(v-1) = k(k-1) = 56$ より定理19.11が使える。

方程式 $z^2 = (k-\lambda)x^2 + (-1)^{(v-1)/2}\lambda y^2$（すなわち $z^2 = 6x^2 + 2y^2$）が非自明な整数解を持つと仮定する。一般性を失わず $\gcd(x,y,z) = 1$ と仮定する。

$y,z$ の少なくともどちらかが $3$ の倍数だった場合、$3 \mid x,y,z$ となり矛盾。そうでない場合 $1 \equiv 0 + 2 \pmod 3$ となり矛盾。

## 問題19M

$M \in \mathbb{Q}^{v \times v}$ について $MM^\top = mI$ であるとする（$m$ は整数）。
1. $v$ が奇数のとき、$m$ が平方数であることを示せ。
2. $v \equiv 2 \pmod 4$ のとき、$m$ が $2$ つの平方数の和であることを示せ。

　

1. 適当に $g$ 倍して分母をはらう。$gM = M' \in \mathbb{Z}^{v \times v}$ とする。$M\'M\'^\top = g^2mI$ より $(\det M')^2 = (g^2m)^v$。
2. [J. H. van Lint and J. J. Seidel (1966), Equilateral point sets in elliptic geometry](https://www.sciencedirect.com/science/article/pii/S1385725866500385) 7ページ目 定理5.2

## Steiner triple system

対称という条件を外し、$2-(v, 3, 1)$ デザインを考える。これを **Steiner triple Sysmtem** といい、$STS(v)$ と書く。

## 定理

$STS(v)$ の存在の必要十分条件は $v \equiv 1,3 \pmod 6$

#### 証明（必要性）

$b = \lambda\dbinom{v}{t} / \dbinom{k}{t} = v(v-1)/6$、$b_1 = \lambda\dbinom{v-1}{t-1}/\dbinom{k-1}{t-1} = (v-1)/2$（定理19.2、定理19.3）

十分性は構成により示す。

### $STS(6t+3)$ の構成（例19.11）

$n = 2t+1$ とおく。

$$
\begin{aligned}
\mathcal{P} &= \mathbb{Z}_n \times \mathbb{Z}_3 \\\\ 
\mathcal{B} &= \\{\\{(x,0),(x,1),(x,2)\\} \mid x \in \mathbb{Z}_n \\} \cup \\{\\{(x,i),(y,i),(\frac{x+y}{2},i+1)\\} \mid x \neq y, i \in \mathbb{Z}_3 \\}
\end{aligned}
$$

### $STS(6t+1)$ の構成（例19.15）

後まわし（文献の順番に従います）

### $v = 6t+1$ が素数ベキである場合（例19.12）

$\alpha$ を $\mathbb{F}_q$ の原始根とする。
$$
\begin{aligned}
\mathcal{P} &= \mathbb{F}_q \\\\ 
\mathcal{B} &= \\{\\{\alpha^i + \xi, \alpha^{2t+1}+\xi, \alpha^{4t+i}+\xi\\} \mid 0 \leq i < t, \xi \in \mathbb{F}_q\\}
\end{aligned}
$$

（メモ）同じブロックに属する元同士の差を見るといい感じになっている

$3 < v < 100$ で $v \equiv 1 \pmod 6$ であるもののうち素数ベキでないものは、$55,85,91$ のみ。

$\not{7},\not{13},\not{19},\not{25},\not{31},\not{37},\not{43},\not{49},55=5\times11,\not{61},\not{67},\not{73},\not{79},85=5\times17,91=7\times13,\not{97}$

### $STS(v_1)$ と $STS(v_2)$ から $STS(v_1v_2)$（例19.13）

それぞれの点集合を $V_1,V_2$ とする。点集合を $V_1 \times V_2$ とし、ブロック集合 $\mathcal{B}$ を次のどれかを満たす $\\{(x_1,y_1),(x_2,y_2),(x_3,y_3)\\}$ の集合とする。

1. $x_1=x_2=x_3$ かつ $\\{y_1,y_2,y_3\\}$ が $STS(v_2)$ のブロックである
2. $\\{x_1,x_2,x_3\\}$ が $STS(v_1)$ のブロックであり、$y_1=y_2=y_3$
3. $\\{x_1,x_2,x_3\\}$ が $STS(v_1)$ のブロックであり、$\\{y_1,y_2,y_3\\}$ が $STS(v_2)$ のブロックである

$STS(7)$ と $STS(13)$ から $STS(91)$ が構成できた。

### $STS(v_1)$、$STS(v)$(?) と $STS(v_2)$ から $STS(v+(v_1-v)v_2)$（例19.14）

点集合 $V_1 = \\{1,\ldots,v_1\\}$、ブロック集合 $S_1$ の $STS(v_1)$ が存在し、$V=\\{v_1-v+1,\ldots,v_1\\}$ と $S_1$ のうち $V$ に含まれるブロックの集合が $STS(v)$ をなすとする。また、点集合 $V_2 = \\{1,\ldots,v_2\\}$、ブロック集合 $S_2$ の $STS(v_2)$ が存在するとする。

点集合は $\mathcal{P} = V \cup \\{(x,y) \mid x \in V_1 \setminus V, y \in V_2\\}$

ブロック集合は次の和集合とする。

1. $STS(v)$ のブロック
2. $\\{(a,y),(b,y),c\\}$、ただし $\\{a,b,c\\} \in S_1$、$c \in V$、$y \in V_2$
3. $\\{(a,y),(b,y),(c,y)\\}$、ただし $\\{a,b,c\\} \in S_1$、$c \not\in V$、$y \in V_2$
4. $\\{(x_1,y_1),(x_2,y_2),(x_3,y_3)\\}$、ただし $x_1+x_2+x_3 \equiv 0 \pmod {v_1-v}$、$\\{y_1,y_2,y_3\\} \in S_2$

$v_1=7$、$v=3$（$STS(7)$ のブロックを $1$ つ選ぶ）、$v_2=13$ として $STS(55)$ が構成できた。（$55 = 3 + 13 \times 4$）

### $STS(v_1)$ と $STS(v_2)$ から $STS(v_1v_2-v_2+1)$ （問題19N(a)）

例19.14 と似た方針をとる。今回は $V = \\{1\\}$ とする。

点集合 $\mathcal{P} = \\{1\\} \cup \\{(x,y) \mid x \in V_1 \setminus \\{1\\}, y \in V_2\\}$

ブロック集合

1. $\\{(a,y),(b,y),c\\}$、ただし $\\{a,b,c\\} \in S_1$、$c = 1$、$y \in V_2$
2. $\\{(a,y),(b,y),(c,y)\\}$、ただし $\\{a,b,c\\} \in S_1$、$c \neq 1$、$y \in V_2$
3. $\\{(x_1,y_1),(x_2,y_2),(x_3,y_3)\\}$、ただし $x_1+x_2+x_3 \equiv 0 \pmod {v_1-1}$、$\\{y_1,y_2,y_3\\} \in S_2$

これにより $STS(7)$ と $STS(13)$ から $STS(85)$ が構成できた。（$85 = 7 \times 12 + 1）

#### 系（問題19N(b)）

この方法で $STS(7)$ と $STS(3)$ から $STS(15)$ が構成できる。このようにして得た $STS(15)$ は Fano plane（$STS(7)$）を subsystem にもつ（ブロック集合を包含する）。

（1. と 2. に該当するブロックのうち $y=1$ のものは、Fano plane のそれになる）

### $STS(6t+1)$ の構成（例19.15）

$\mathcal{P} = \mathbb{Z}_{2t} \times \mathbb{Z}_3 \cup \\{\infty\\}$ とする。

$\mathcal{P}$ に加法を要素ごとの和として定義する。ただし $\infty + (x,i) = \infty$。また、簡単のために以下では $(x,i)$ を $x_i$ と表記する。

次のものを「基本ブロック」とする。

1. $\\{0_0, 0_1, 0_2\\}$
2. $\\{\infty, 0_0, t_1\\}$, $\\{\infty, 0_1, t_2\\}$, $\\{\infty, 0_2, t_0\\}$
3. $\\{0_0, i_1, (-i)_1\\}$, $\\{0_1, i_2, (-i)_2\\}$, $\\{0_2, i_0, (-i)_0\\}$（$i=1,\ldots,t-1$）
4. $\\{t_0, i_1, (1-i)_1\\}$, $\\{t_1, i_2, (1-i)_2\\}$, $\\{t_2, i_0, (1-i)_0\\}$（$i=1,\ldots,t$）

（全部で $6t+1$ 個）

各 $0 \leq a \leq t-1$ について、各基本ブロックの各要素に $a_0$ を加えてできる、合計 $t(6t+1)$ 個のブロックの集合を $\mathcal{B}$ とすると、$STS(6t+1)$ が構成される。

　

---

　

## write-once メモリと $STS(7)$

セルの値を $0$ から $1$ に変更できるが、$1$ から $0$ には変更できないメモリがある。（パンチカード、CDなど）

$1$ から $7$ の整数を何度か書き込む。このときメモリ領域をできるだけ使い回すことを考える。

（お絵描き）

　

---

　

### 問題19O

１．集合族 $\mathcal{A} \subset 2^{[n]}$ について、任意の $S \in \mathcal{A}$ について $|S|$ が奇数であり、任意の $S,T \in \mathcal{A}, S \neq T$ について $|S \cap T|$ が偶数であるとする。$|\mathcal{A}| \leq n$ を示せ。

２．任意の $S \in \mathcal{A}$ について $|S|$ が偶数であり、任意の $S,T \in \mathcal{A},S \neq T$ について $|S \cap T|$ が奇数であるとき、$|\mathcal{A}| \leq n+1$ であることを示せ。等号が成立する例を挙げよ。

　

追いついていません。$b=|\mathcal{A}|$ として $\mathcal{A}$ の接続行列を $N \in \mathbb{F}_2^{n \times b}$ とすると $N^\top N = I$ というようなことがヒントにはあります。

### 問題19P

$v = \binom{k+1}{2}$ として $2$-$(v,k,\lambda=2)$ デザインを考える。

１．$k=3$ の場合の例を挙げよ。

２．ブロックを $A_1,A_2,\ldots,A_b$ とし、各 $i=2,3,\ldots,b$ について $\mu_i = |A_i \cap A_1|$ とする。次の値を求めよ。

$$ \sum_{i=2}^b \mu_i,\quad \sum_{i=2}^b \mu_i(\mu_i-1),\quad \sum_{i=2}^b (\mu_i-1)(\mu_i-2) $$

　

１．お絵描き

２-１：$A_1$ の各元ごとに寄与を考えると $\sum_{i=2}^b \mu_i = k(b_1-1)$。定理19.3 より

$$ b_1 = \lambda \binom{v-1}{t-1} / \binom{k-1}{t-1} = 2 \binom{\binom{k+1}{2}-1}{1} / \binom{k-1}{1} = \frac{(k+1)k-2}{k-1} = k+2 $$

よって $\sum_{i=2}^b \mu_i = k(k+1)$

２-２：任意の相異なる元 $a,b \in A_1$ について $(a,b)$ の寄与は $b_2-1$。定理19.3 より

$$ b_2 = \lambda \binom{v-2}{t-2} / \binom{k-2}{t-2} = 2 \binom{v-2}{0} / \binom{k-2}{0} = 2 $$

よって $\sum_{i=2}^b \mu_i(\mu_i-1) = k(k-1)$

２-３：定理19.2 より

$$
\begin{aligned}
b &= \lambda \binom{v}{t}/\binom{k}{t} = 2 \binom{\binom{k+1}{2}}{2} / \binom{k}{2} \\\\ 
  &= 2 \frac{((k+1)k/2)((k+1)k/2-1)}{2}\frac{2}{k(k-1)} \\\\ 
  &= \frac{(k+1)k}{2}\frac{(k+2)(k-1)}{2}\frac{2}{k(k-1)} \\\\ 
  &= \frac{(k+1)(k+2)}{2}
\end{aligned}
$$

$\sum_{i=2}^b \mu_i = k(k+1)$, $\sum_{i=2}^b \mu_i^2 - \sum_{i=2}^b \mu_i = k(k-1)$ が分かっているので、

$$
\begin{aligned}
\sum_{i=2}^b (\mu_i-1)(\mu_i-2) &= \sum_{i=2}^b \mu_i^2 - 3\sum_{i=2}^b \mu_i + 2(b-1) \\\\ 
  &= k(k-1) - 2k(k+1) + 2((k+1)(k+2)/2-1) \\\\ 
  &= k^2 - k - 2k^2 - 2k + k^2 + 3k + 2 - 2 \\\\ 
  &= 0
\end{aligned}
$$

和は $\geq 0$ なので、各 $\mu_i$ は $1,2$ のどちらかである。

### 問題19Q

Steiner System $S(t,k,v)$ から「各ブロックのサイズが $k$ で一定」という条件を外した、一般 Steiner System を考える。$b=1$ の自明なケースは除くこととする。

非自明な一般 Steiner System の $b$ の最小値を $b_{t,v}$ で表すとき、$t \geq 2$ について

$$ b_{t,v}(b_{t,v}-1) \geq t\binom{v}{t} $$

を示せ。（これよりずっと強い下界が知られているが、導出は難しいらしい）

　

$t$ の帰納法で示す。$t=2$ の場合は定理19.1 が使える。

> 線形空間（どのブロックも $2$ 個以上の点と接続し、どの $2$ 個の点もちょうど $1$ 個のブロックにともに属する）において、$b=1$ または $b \geq v$

（追記：$b$ の最小値を考えているので、$|B|=1$ であるようなブロック $B \in \mathcal{B}$ はないものとしてよい）$t=2$ の一般 Steiner System は線形空間である。目的の不等式 $b_{2,v}(b_{2,v}-1) \geq v(v-1)$ は、$b \geq v$ より示される。

$t$ の場合が示されているとし、$t+1$ の場合を考える。$t+1$ の一般 Steiner System にて、$A,B$ が相異なるブロックで $x \in A,B$ であるような組 $(x, A, B)$ の個数を $n$ とする。

1. 任意の相異なるブロック $A,B$ について $|A \cap B| < t+1$ ゆえ $n \leq tb(b-1)$
2. $t+1$ の一般 Steiner System の点集合 $\mathcal{P} \ni x$、ブロック集合 $\mathcal{B}$ について、$$(\mathcal{P} \setminus \\{x\\}, \\{B \setminus \\{x\\} \mid B \in \mathcal{B}, x \in B\\})$$ は $t$ の一般 Steiner System をなす。（誘導デザインのようなもの）$\\\\$
  ここから $2$ つの相異なるブロック $A',B'$ をとって $(x, A'\cup\\{x\\}, B'\cup\\{x\\})$ とすることを考えると、$n \geq vb_{t,v}(b_{t,v}-1)$ $\\\\$
  ここで帰納法の仮定より $$vb_{t,v}(b_{t,v}-1) \geq vt\binom{v}{t} = \frac{vt(t+1)}{v-t}\binom{v}{t+1} $$
  これより$n \geq t(t+1)\binom{v}{t+1}$　（タイトでないので合っているか不安）

これらより $b(b-1) \geq (t+1)\binom{v}{t+1}$ が示された。

### 問題19R

Fano plane のブロック集合の個別代表系を数えよ。

　

$v \times b$ の接続行列：

$$
\begin{pmatrix}
1 & 1 & 1 & 0 & 0 & 0 & 0 \\\\ 
1 & 0 & 0 & 1 & 0 & 1 & 0 \\\\ 
0 & 1 & 0 & 1 & 1 & 0 & 0 \\\\ 
0 & 0 & 1 & 0 & 1 & 1 & 0 \\\\ 
1 & 0 & 0 & 0 & 1 & 0 & 1 \\\\ 
0 & 1 & 0 & 0 & 0 & 1 & 1 \\\\ 
0 & 0 & 1 & 1 & 0 & 0 & 1
\end{pmatrix}
$$

$24$ 個

### 問題19S

すべての $k \geq 2$ について $3$-$(2^k,4,1)$ デザインを構成せよ。

　

$\mathbb{F}_2^k$ を点集合にとり、相異なる $x,y,z$ について $x+y+z+w \equal 0$ となるような $\\{x,y,z,w\\}$ すべてをブロック集合にとる。（たとえば $x=w$ とすると $y=z$ となり矛盾なのでOK）

### 問題19T

あるデザインが他の誘導デザインであるとき、「拡張可能である」という。対称デザインであって $2$ 回拡張可能であるものは $2$-$(21,5,1)$ のみであることを示せ。

> 点集合が $\mathcal{P}$、ブロック集合が $\mathcal{B}$ の $t$-$(v,k,\lambda)$ デザイン $\mathcal{D}$ に対し、$|I| \leq t$ であるような $I \subset \mathcal{P}$ をとって、点集合を $\mathcal{P} \setminus I$、ブロック集合を $\\{B \setminus I \mid B \supset I\\}$ とすると、これは $(t-i)$-$(v-i,k-i,\lambda)$ デザインをなす。これを $\mathcal{D}$ の誘導デザインという。

　

わからず。問題19H が使えるらしい。

### 問題19U

問題1J で登場したグラフ $G = (V, E)$ を考える。点集合を $V$、ブロック集合を $\\{\Gamma(x) \mid x \in V\\}$ としたデザインは射影平面であることを示せ。

> $G$ を頂点数が $n \geq 3$ でありどの頂点も次数が $n-1$ でない単純グラフとする。また、任意の $2$ 頂点についてその両方に隣接する頂点がただ $1$ つ存在するとする。
> 1. $x,y \in V$ が隣接していないとき、これらの次数が等しいことを示せ。
> 2. $G$ が正則であることを示せ。

当時「そのようなグラフは存在しないのでは」というような話になった気が…　問題21Q でも出てくるらしい

　

問題1J の結果からブロックの位数はすべて等しく、任意の $2$ 点 $x,y$ について、それらがともに接続するブロックがちょうど $1$ つ（$x,y$ 両方に隣接する頂点 $z$ について $\Gamma(z)$）存在する。

$2$-デザインで $v=b$ であり、$\lambda=1$ であるからこれは射影平面である。

### 問題19V

定理19.8 の記法を用いる。
1. $W_{is}N_s=\binom{k-i}{s-i}N_i$ を示せ。
2. $W_{0s}^\top W_{0s},W_{1s}^\top W_{1s},\ldots,W_{ss}^\top W_{ss}$ のうちどの $2$ つの積も、これら $s+1$ 個の行列の線型結合であることを示せ。
3. 定理19.8 の等号が成立するならば、$N_s$ が正方行列であることと、$M = \sum_{i=0}^s b_{2s-i}^i W_{is}^\top W_{is}$ として $N_s^\top M^{-1} N_s = I$ であることを示せ。
  $M \in \mathcal{A}$ であるから、2. より $M^{-1} \in \mathcal{A}$ である。これを用いて、任意の相異なるブロック $A,B$ について $f(|A \cap B|) = 0$ であるような、次数 $s$ の多項式 $f(x)$ が存在することを示せ。

　

分かりませんでした。
