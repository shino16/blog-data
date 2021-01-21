---
title: "Tonelli Shanks"
date: 2020-10-26T00:14:45+09:00
draft: true
---

Project Eulerで解いた問題の解説に出てきたので，この機会にまとめておく．

Tonelli–Shanksのアルゴリズムの話は[ここ](#Tonelli–Shanksのアルゴリズム)から

## 平方剰余とは

ある正整数を法としたときの平方数を**平方剰余**という．たとえば，法を$3$とすると$1$は平方剰余（$1^2 \equiv 2^2 \equiv 1$）であり，$2$は平方剰余ではない．

### モチベーション

たとえば，有名なディオファントス方程式$a^2 + b^2 = c^2$において$\pmod 4$をとると，$a,b$がともに奇数であったとき左辺は$2$となるが，これは平方剰余でないので不適，ゆえに$a,b$のどちらかは偶数．

この平方剰余について成り立つ法則を調べることで，このようにして方程式の整数解について調べたり，例えば$p \mid an^2+b$となる条件を調べたりしたい．

以上自分が思いついたものを挙げてみた．

## Legendre記号

ここで便利のために，整数$a$と**奇素数**$p$に対して**Legendre（ルジャンドル）記号**を導入する．

$$
\left(\dfrac{a}{p}\right) = \begin{cases}
    1 & (a \not\equiv 0 \land \text{$a$は$p$を法とする平方剰余}) \\
    -1 & (\text{$a$は$p$を法とする平方剰余でない}) \\
    0 & (a \equiv 0)
\end{cases}
$$

## Eulerの規準

なんと

$$ \left(\dfrac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod p $$

証明は[英語版Wikipedia](https://en.wikipedia.org/wiki/Euler%27s_criterion)にも載っている．ざっくり説明すると，以下$a \not\equiv 0$であるとしたとき，まずこの右辺のとりうる値は$\pm1$のどちらか（フェルマーの小定理より，$2$乗して$1$になるので）．方程式$a^{\frac{p-1}{2}} \equiv 1 \pmod p$を考えたとき，$x^2 \equiv a$ならば左辺$\equiv x^{p-1} \equiv 1$なので平方剰余はすべて解であるが，式の次数から解の個数は$\frac{p-1}{2}$以下，また$0$でない相異なる平方剰余は$1^2,2^2,\ldots,(\frac{p-1}{2})^2$のちょうど$\frac{p-1}{2}$個あるので，最初の方程式の解の集合に一致することがわかる．解でない$a \not\equiv 0$については左辺$\equiv -1$．という感じでしょうか．

この議論から，奇素数$p$について平方剰余と平方非剰余の個数が等しいこともわかる．

Eulerの規準を使うことで，二分累乗法により時間計算量$O(\log p)$で判定できる．

### 乗法性

上の事実からこのことがすぐにいえる．

$$ \left(\dfrac{mn}{p}\right) = \left(\dfrac{m}{p}\right) \left(\dfrac{m}{p}\right) $$

奇素数を法として平方非剰余$2$個の積をとると平方剰余になるというのはちょっと不思議．

たとえば$p$未満の各正整数について最小の素因数を求めておけば（[参考](https://cp-algorithms.com/algebra/prime-sieve-linear.html)），各$n$に対する$\left(\dfrac{n}{p}\right)$が$O(p + \pi(p)\log p)$（$\pi(n)$は$n$以下の素数の個数）で計算できるはず．素数定理より$\pi(n) \approx n/\log n$なので$O(p)$に収まっているといえる．合ってるよね

## 便利な法則

以下の法則を使うこともできる．

* 平方剰余の相互法則

$$ \left(\dfrac{p}{q}\right) \left(\dfrac{q}{p}\right) = (-1)^{\frac{p-1}{2}\frac{q-1}{2}} $$

* 第一補充法則

$$ \left(\dfrac{-1}{p}\right) = (-1)^{\frac{p-1}{2}} $$

* 第二補充法則

$$ \left(\dfrac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}} $$

第一補充法則はEulerの規準において$a=-1$とした場合．第二補充法則・平方剰余の相互法則の証明は[Wikipedia](https://en.wikipedia.org/wiki/Quadratic_reciprocity#Proof)へ．上下を逆転できるのはおもしろい．

Eulerの規準と比べて，$a$に対して$\left(\dfrac{a}{p}\right)=1$であるような$p$を探したいといったときに役に立ちそう．手計算もこちらの方が楽かもしれない？　どうだろう．

これらを使って$\left(\dfrac{14}{19}\right)$を計算する例が[高校数学の美しい物語](https://mathtrain.jp/sogohosoku)に，$\left(\dfrac{12345}{331}\right)$の例が[Wikipedia](https://en.wikipedia.org/wiki/Legendre_symbol#Computational_example)にある．

## Tonelli–Shanksのアルゴリズム

以上の方法で$n \not\equiv 0$が素数$p$を法とする平方剰余であることが分かったとして，$x^2 \equiv n \pmod p$の解を求めてみよう．

（追記）下は単に残してあるだけです　37zigenさんによるこちらの記事を見ましょう！[https://37zigen.com/tonelli-shank-のアルゴリズム](https://37zigen.com/tonelli-shank-のアルゴリズム)

まず，何らかの方法で$R$が解であると予想したとする．ある$t$が存在して$R^2 \equiv nt \pmod p$とおける．この条件式を満たし続けるように$(R, t)$を置き換えていき，最終的に$t \equiv 1$にできれば勝ち．

ここでオイラーの規準より$1 \equiv n^{\frac{p-1}{2}}$であることを念頭におくと，$R^2$の形を$n \cdot n^{\frac{p-1}2}$に近づけるために以下のことを思いつくかもしれない．（え？）

$Q$をある奇数として$p-1 = Q2^S$とおく（このようなおき方がちょうど$1$通り存在する）．$R \equiv n^{\frac{Q+1}{2}}$とおく．こうすると，$R^2 \equiv n^{Q+1}$から$t \equiv n^Q$．$1 \equiv n^{\frac{p-1}{2}} \equiv n^{Q2^{S-1}} \equiv t^{2^{S-1}}$，すなわち$t$は$1$の$2^{S-1}$乗根であることが見てとれる．

ということは，$z$を$1$の原始$2^S$乗根とおくと（$z^2$は原始$2^{S-1}$乗根），ある非負整数$k$が存在して$z^{2k}t \equiv 1$，よって$R,t$にそれぞれ$z^k,z^{2k}$を掛ければ$R^2 \equiv nt$かつ$t \equiv 1$となり，つまり求める解にたどりつく．

この$z$は，オイラーの規準を使うとすぐに手に入れられる．$\frac{p-1}{2}$個ある平方非剰余を$1$つとって$b$とすると，$b^{\frac{p-1}{2}} = b^{Q2^{S-1}} \equiv -1$から$z=b^Q$とすればよい．$1,\ldots,p-1$からランダムに選んで判定することを繰り返せば，平均$2$回で平方非剰余に当たると見込める．

あとは$z^{2k}t\equiv1$となるような$z^{2k}$を見つければよい．これは高々$k$回$z^2$を掛けていくことで実現できるが，**二分累乗法**が適用できる．$1$の原始$2^M$乗根$z_M=z^{2^{S-M}}$をおいておく．

いま$t$が$1$の$2^M$乗根であることが分かっているとする．$(t^{2^{M-1}})^2 \equiv 1$より$t^{2^{M-1}} \equiv \pm 1$であり，これが$+1$ならば$t$はそのまま$2^{M-1}$乗根である．そうでない場合，$(z_Mt)^{2^{M-1}} \equiv 1$より，$z_{M+1}$を$R$に，$z_M=z_{M+1}^2$を$t$に掛ければ，$t$が$2^{M-1}$乗根であるような$(R, t)$を得ることができる．

これを各$M=S-1,S-2,\ldots,1$について行えば，$t$は$1$の$2^0$乗根$\equiv1$となり，$R^2 \equiv n$を満たす$R$が手に入る．以上がTonelli–Shanksのアルゴリズム．

kikira_compさんの[整数論テクニック](http://kirika-comp.hatenablog.com/entry/2018/03/12/210446)の$14$ページに群論の言葉での説明があるけど、自分にはよくわからず…もっと勉強してから戻ってくるつもり．

## C++での実装

```cpp
#include <cstdlib>
#include <cstdint>
using ll = long long;

ll modpow(ll base, ll exp, ll mod) {
  ll ret = 1;
  for (; exp; exp /= 2, (base *= base) %= mod)
    if (exp % 2) (ret *= base) %= mod;
  return ret;
}

ll tonelli_shanks(ll n, ll p) {
  ll b = rand() % p;
  while (modpow(b, (p-1)/2, p) != p-1) b = rand() % p;

  int S = __builtin_ctzll(p-1);
  ll Q = (p-1) >> S;
  ll R = modpow(n, (Q+1)/2, p);
  ll t = modpow(n, Q, p);
  ll z = modpow(b, Q, p);

  for (int M = S-1; M > 0; M--, (z *= z) %= p) {
    if (modpow(t, 1<<(M-1), p) == p-1)
      (R *= z) %= p, (t *= z * z % p) %= p;
  }

  return R;
}
```

時間計算量は$O(\log^2 p)$．お疲れさまでした．

## 参考文献

[平方剰余と基本的な問題](https://mathtrain.jp/joyo)，高校数学の美しい物語

[Euler's criterion](https://en.wikipedia.org/wiki/Euler%27s_criterion), Wikipedia

[Legendre Symbol](https://en.wikipedia.org/wiki/Legendre_symbol), Wikipedia

[平方剰余の相互法則の意味と応用](https://mathtrain.jp/sogohosoku), 高校数学の美しい物語

[Tonelli–Shanks algorithm](https://en.wikipedia.org/wiki/Tonelli%E2%80%93Shanks_algorithm), Wikipedia

[整数論テクニック](http://kirika-comp.hatenablog.com/entry/2018/03/12/210446), kirika_compのブログ

ありがとうございました．
