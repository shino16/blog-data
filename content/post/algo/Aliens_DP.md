---
title: "Aliens DP の視覚的な説明と出題例"
date: 2023-11-28T02:30:00+00:00
tag:
- DP
---

Aliens DP (the trick from Aliens) を解説します．

定義や記号は [noshi91 さんの記事](https://noshi91.hatenablog.com/#fn-aeff7d60) に概ね準拠しています．Aliens DP の使い方はこの記事に書いてあることが全てなので，何をしたいかが分かればこの記事を見てください．

## 例

何かをちょうど $k$ 回使うとして，コスト $f(k)$ を最小化する DP を考えます．求めたいものが $\operatorname{dp}[n][k]$ だとすると，状態数は $O(nk)$ です．これを高速化します．

「ちょうど $k$ 回使う」という制約を一旦忘れ，代わりに「$1$ 回使うたびにコストを $p$ 減らせる」という状況を考えます．つまり，$f(x)$ の代わりに $g(p) = \min_x (f(x)-px)$ の最小化を考えます．与えられた $p$ に対する $g(p)$ の計算では，DP の次元が一つ落ち，状態数が $O(n)$ になって速いです．

$p$ が $\infty$ に近づくと，$f(x)-px$ を最小化する $x$ は大きくなり，$p$ が $-\infty$ に近づくと $x$ は小さくなります．ここで **$f$ が凸と仮定すると**，$p$ をちょうど良い塩梅 $p=\tilde p$ に決めれば $x=k$ が $f(x)-\tilde p x$ を最小化します．言い換えると，$g(\tilde p) = \min_x(f(x)-\tilde p x) = f(k)-\tilde p k$ を満たす $\tilde p$ が存在します（後述）．

そのような $\tilde p$ は二分探索/三分探索で発見でき（後述），$f(k) = \tilde p k+g(\tilde p)$ が求まります．すごい．

## $\tilde p$ の存在

以降では $f$ の凸性を仮定します．本来 $f(x)$ は整数 $x$ に対してのみ定義されていますが，線分で補間して折れ線とみなします．

$g(p) = \min_x(f(x)-px)$ は傾き $p$ であるような $f$ の接線の $y$ 切片を与えます（$f$ は微分不可能な点を持ちますが，それっぽいやつ）．

下図を参照してください．オレンジ色の直線が $f$ の接線です．

<iframe src="https://www.geogebra.org/calculator/d5v6ww2j?embed" width="800" height="600" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

$f$ の $x=k$ における傾きを $\tilde p$ にとれば，$x=k$ が $f(x)-\tilde px$ を最小化することになります（ここで凸性を使った）．

## $\tilde p$ の探索

$\tilde p$ を発見する方法を考えます．

$p$ を適当に選び $g(p)$ を計算すると，傾き $p$ の接線（下図オレンジ色の直線）が分かり，特に $pk+g(p)$ を求めることができます（下図ピンク色の点）．

<iframe src="https://www.geogebra.org/calculator/snebamzy?embed" width="800" height="600" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

$f$ の接線は $f$ の下側にある（凸性）ので，$pk+g(p) \leq f(k)$ です．欲しいものは $g(\tilde p) = f(k)-\tilde p k$ を満たす $\tilde p$ であり，$\tilde p k + g(\tilde p) = f(k)$ であることから，$pk+g(p)$ を最大化すればよいです．

$g(p)=\min_x(f(x)-px)$ は $p$ に関する線形関数の $\min$ なので凹であり，$pk+g(p)$ も凹なので，三分探索/黄金分割探索で $\tilde p$ が発見できます．以上です．

## 二分探索を使う方法

$g(p) = \min_x(f(x)-px)$ を何らかの方法 (DP) で求めるとき，この最小化を達成する $x_p^\* \in \operatorname{argmin}_x(f(x)-px)$ が一緒に求められるとします (DP の復元で可能)．

$(x_p^\*, f(x_p^\*))$（下図ピンク色の点）は傾き $p$ の接線との接点であり，$x_p^\*$ は $p$ について単調です．$x_p^\*=k$ となるように $p$ を二分探索すれば自動的に $f(x_p^\*)=f(k)$ が求まります．

<iframe src="https://www.geogebra.org/calculator/kexxmzfs?embed" width="800" height="600" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

なお，$x_p^\*$ を $\operatorname{argmin}_x(f(x)-px)$ の中からどのように選ぶかを決めておくことや，二分探索の境界条件に関する注意が必要です．詳細は [noshi91 さんの記事](https://noshi91.hatenablog.com/#%E3%83%9A%E3%83%8A%E3%83%AB%E3%83%86%E3%82%A3%E5%9B%9E%E6%95%B0%E3%81%AE%E7%AE%A1%E7%90%86) を参照してください．

## 変種：$f^{-1}(k)$ を求める

細かい話は省きますが，同じことをするだけです．接線が分かれば直線 $y=k$ との交点が分かるので三分探索ができ，さらに接点 $(x^\*_p, f(x^\*_p))$ が分かれば二分探索もできます．$p$ の範囲は正です．

<iframe src="https://www.geogebra.org/calculator/hdkypgxb?embed" width="800" height="600" allowfullscreen style="border: 1px solid #e4e4e4;border-radius: 4px;" frameborder="0"></iframe>

## 実装に関して

[noshi91 さんの記事](https://noshi91.hatenablog.com/#fn-aeff7d60) を参照してください．

$f$ の値が整数なら，$p$ も整数のものだけ考えればよいです．

## その他

**凸性の証明**

$f\colon \mathbb{Z} \to \mathbb{R}$ が凸であることを示すには，$2f(x) \geq f(x-1)+f(x+1)$（または $f(x)-f(x-1) \geq f(x+1)+f(x)$）が言えれば十分です．「$x$ が元々大きいと $1$ 増やすのももっと大変だよね」という議論だけでは厳密には足りていません．よくある証明パターンは，$x-1$ に対する構成と $x+1$ に対する構成を部分的に組み替えて $x$ に対する構成を $2$ つ作ることです．

**定義域について**

本記事では $f$ の定義域が有界でしたが，端に $\infty$ を詰めれば $\mathbb{R}$ 全体に対して $f$ を定義できます．こうして得た $f$ も凸性を保ちます．

**Monge について**

Aliens DP を適用するにあたってコストが Monge であることは必要ではありませんが，Monge $\implies$ 凸 は成立します．[参照](https://noshi91.github.io/algorithm-encyclopedia/d-edge-shortest-path-monge)

**$f(k)$ ではなく $\min\{f(x): a \leq x \leq b\}$ を求めたい**

別の [noshi91 さんの記事](https://noshi91.hatenablog.com/entry/2022/01/13/001217) を参照してください．

## 問題例

* [ECR79 F](https://codeforces.com/contest/1279/problem/F)

やるだけ．凸性の証明も典型っぽい？

* [ABC218 H](https://atcoder.jp/contests/abc218/tasks/abc218_h)

同様．解説が $3$ つとも非常に参考になった．

* [ARC168 E](https://atcoder.jp/contests/arc168/tasks/arc168_e)

最近の問題．Monge ではないが凸だと話題になっていた．

* [IOI2016 Aliens](https://www2.ioi-jp.org/ioi/2016/tasks/day2-aliens-JPN.pdf) [Luogu](https://www.luogu.com.cn/problem/P5896)

Aliens という名前の由来となった問題．難しそう．

[Codeforces の一連のコメント](https://codeforces.com/blog/entry/49691?#comment-402753) によると，この問題が出題される何年も前に中国ではこのようなテクニックが一部で知られていたらしい．その人の名前のイニシャルを取って，中国では "WQS binary search" と呼ばれているようだ．
