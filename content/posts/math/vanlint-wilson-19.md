---
title: "Vanlint Wilson 19"
date: 2020-10-30T14:25:20+09:00
# draft: true
hidden: true
tags:
- 数学
---


## 例19.10

定理19.11 を使ってみましょう

### オーダー $n = 6$ の射影平面（$\lambda=1$ の symmetric design）

※ $n=2,3,4,5,7,8,9$ の場合は $F_n$ を使って $PG_2(n)$ が構成できる

※ $v = n^2+n+1, k=n+1, \lambda=1$ $\quad \therefore \ \lambda(v-1)=k(k-1)=n^2+n$

$v$ は奇数より、$z^2 = (k-\lambda)x^2 + (-1)^{(v-1)/2}\lambda y^2$（すなわち $z^2 = 6x^2 - y^2$) を満たす非零の整数解の存在が必要。

そのような解が存在すると仮定する。一般性を失わず $\gcd(x,y,z)=1$ を仮定する（$x,y,z$ をそれぞれ $\gcd(x,y,z)$ で割ったものを考える）。

$y,z$: 奇数 より $y^2 \equiv z^2 \equiv 1 \pmod 8$。$6x^2 \equiv 0,6 \pmod 8$ より矛盾。

※ $n^2 \equiv 0,1 \pmod 8$、$n$ が奇数なら $n^2 \equiv 1 \pmod 8$、下図参照

|$n$|0|1|2|3|4|5|6|7|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|$n^2 \bmod 8$|0|1|4|1|0|1|4|1|

### オーダー $10$ の射影平面

$z^2 = 10x^2 - y^2$ は解 $(x,y,z) = (1,1,3)$ を持つため、定理19.11は使えない。

オーダー $10$ の射影平面が存在しないことが1989年にコンピュータによる探索で示された（定理19.11以外の方法で非存在が示された唯一の例）。

## 系

オーダー $n \equiv 1, 2 \pmod 4$ の射影平面が存在するならば、$n$ は $2$ つの平方数の和である。

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

  ※ $N(z) = z\overline{z}$、$N(z)N(\lambda\dbignom{v-1}{t-1}/\dbinom{k-1}{t-1} = w) = N(zw)$

* **ユークリッド除法** 任意の $a,b \in \mathbb{Z}[i]$ $(b \neq 0)$ について、$a = bq+r$ かつ $N(r) < N(b)$ を満たす $q,r \in \mathbb{Z}[i]$ が存在する。

  ※ 複素数平面において $\frac{a}{b}$ に最も近いガウス整数を $q$ とおくと、$$\left|\frac{a}{b}-q\right| \leq \frac{1}{\sqrt{2}}$$ より $$N(r) = N(a-bq) = N(b)N\left(\frac{a}{b}-q\right) \leq \frac{N(b)}{2}$$

これらを使って**ガウス素数**や**素因数分解の一意性**といった概念が成立する。（ガウス整数環はユークリッド環であるので一意分解環）

$p \neq \pm 1, \pm i$ がガウス素数であるとは、$p$ が自明な約数 $\pm 1, \pm i, \pm p, \pm pi$ 以外の約数を持たないことをいう。

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

**証明** 帰納的に示す。$n = 1$ のとき明らか。$1, \ldots, n-1$ について示されており、素数 $p \equiv 3 \pmod 4$ について $p \mid n = a^2 + b^2$ であるとき、$p \mid a$、$p \mid\lambda\dbignom{v-1}{t-1}/\dbinom{k-1}{t-1} =  b$ より $p^2 \mid n$ であり、$n/p^2$ の場合に帰着される。

#### 補題（平方剰余の相互法則 第一補充法則）

$p \equiv 1 \pmod 4$ のとき、ある $x \in \mathbb{Z}/p\mathbb{Z}$ が存在して $x^2 \equiv -1 \pmod p$。

**証明** $x = (\frac{p-1}{2})!$ とおくと、$$\begin{aligned}(p-1)! &\equiv (\frac{-p+1}{2})(\frac{-p+3}{2})\cdots(-1)(1)\cdots(\frac{p-1}{2}) \\\\ &\equiv (-1)^{(p-1)/2}x^2 \pmod p \end{aligned}$$

$frac{p-1}{2}$ は偶数であり、$(p-1)! \equiv -1 \pmod p$（ウィルソンの定理）であるから $x^2 \equiv -1 \pmod p$

#### 補題

素数 $p \not\equiv 3 \pmod 4$ はガウス素数ではない。

**証明** $p = 2$ の場合は $2 = (1+i)(1-i)$ より明らか。

$p \equiv 1 \pmod 4$ がガウス素数と仮定する。ある $x$ が存在して $p \mid x^2+1 = (x+i)(x-i)$ より $p \mid x+i$ または $p \mid x-i$ だが、どちらも成り立たず矛盾。

#### 補題（フェルマーの二平方定理）

素数 $p \not\equiv 3 \pmod 4$ は $2$ つの平方数の和である。

**証明** 非自明な $p$ の約数 $a+bi$ について $N(a+bi) = a^2 + b^2 = p$。

#### 補題

$n, m$ が $2$ つの平方数の和ならば、$nm$ も $2$ つの平方数の和である。

**証明** $n = a^2+b^2$、$m = c^\lambda\dbignom{v-1}{t-1}/\dbinom{k-1}{t-1} = 2 + d^2$ とおく。

$$ nm = (a^2+b^2)(c^2+d^2) = (ac-bd)^2+(ad+bc)^2 $$

※ ブラーマグプタ-フィボナッチ恒等式と呼ばれる。$N(a+bi)N(c+di) = N((a+bi)(c+di))$ とも説明できる。

#### 補題 $(\Longleftarrow)$

任意の正整数 $n$ について、任意の素数 $p \equiv 3 \pmod 4$ が $n$ をちょうど偶数回割り切るならば、$n$ は $2$ つの平方数の和である。

## 問題 19L

対称 $2-(29, 8, 2)$ デザインは存在しない。

#### 証明

$\lambda(v-1) = k(k-1) = 56$ より定理19.11が使える。

方程式 $z^2 = (k-\lambda)x^2 + (-1)^{(v-1)/2}\lambda y^2$（すなわち $z^2 = 6x^2 + 2y^2$）が非自明な整数解を持つと仮定する。一般性を失わず $\gcd(x,y,z) = 1$ と仮定する。

$y,z$ の少なくともどちらかが $3$ の倍数だった場合、$3 \mid x,y,z$ となり矛盾。そうでない場合 $1 \equiv 0 + 2 \pmod 3$ となり矛盾。

## 問題19M

[J. H. van Lint and J. J. Seidel (1966), Equilateral point sets in elliptic geometry](https://www.sciencedirect.com/science/article/pii/S1385725866500385) 7ページ目 定理5.2

## Steiner triple system

対称という条件を外し、$2-(v, 3, 1)$ デザインを考える。これを **Steiner triple Sysmtem** といい、$STS(v)$ と書く。

## 定理

$STS(v)$ の存在の必要十分条件は $v \equiv 1,3 \pmod 6$

#### 証明（必要性）

$b = \lambda\dbinom{v}{t} / \dbinom{k}{t} = v(v-1)/6$、$b_1 = \lambda\dbinom{v-1}{t-1}/\dbinom{k-1}{t-1} = (v-1)/2$（定理19.2、定理19.3）

十分性は構成により示す。

#### $v \equiv 3 \pmod 6$ の構成（例19.11）

$STS(6t+3)$ を構成する。$n = 2t+1$ とおく。

$$
\begin{aligned}
\mathcal{P} &= \mathbb{Z}_n \times \mathbb{Z}_3 \\\\ 
\mathcal{B} &= \\{\\{(x,0),(x,1),(x,2)\\} \mid x \in \mathbb{Z}_n \\} \cup \\{\\{(x,i),(y,i),(\frac{x+y}{2},i+1)\\} \mid x \neq y, i \in \mathbb{Z}_3 \\}
\end{aligned}
$$

#### $v \equiv 1 \pmod 6$ の構成（例19.15）

$STS(6t+1)$ を構成する。$\mathcal{P} = \mathbb{Z}_{2t} \times \mathbb{Z}_3 \cup \\{\infty\\}$ とする。

$\mathcal{P}$ に加法を要素ごとの和として定義する。ただし $\infty + (x,i) = \infty$。また、簡単のために以下では $(x,i)$ を $x_i$ と表記する。

次のものを「基本ブロック」と呼ぶ。

$$\begin{aligned}
\mathcal{B}' &= \\{\\{0_0, 0_1, 0_2\\}\\} \\\\ 
&\cup \\{\\{\infty, 0_j, t_{j+1}\\} \mid j\\} \\\\ 
&\cup \\{\\{0_j, i_{j+1}, (-i)_{j+1}\\} \mid 1 \leq i \leq t-1, j\\} \\\\ 
&\cup \\{\\{t_j, i_{j+1}, (1-i)_{j+1}\\} \mid 1 \leq i \leq t, j \\}
\end{aligned}$$

（ここで $|\mathcal{B}'| = 6t+1$）

各 $0 \leq a \leq t-1$ について、基本ブロックの各要素に $a_0$ を加えてできる $t(6t+1)$ 個のブロックの集合を $\mathcal{B}$ とする。

（例19.12～例19.14、問題19Nは追加の条件つきでのいろいろな構成の紹介）

## write-once メモリと $STS(7)$

セルの値を $0$ から $1$ に変更できるが、$1$ から $0$ には変更できないメモリがある。（パンチカード、CDなど）

$1$ から $7$ の整数を何度か書き込む。このときメモリ領域をできるだけ使い回すことを考える。
