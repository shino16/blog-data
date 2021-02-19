---
title: "みんプロ2019 E - Odd Subrectangles"
date: 2021-02-19T15:29:27+09:00
categories:
- "問題"
tags:
- "問題"
- "数学"
- "線型代数"
- "数え上げ"
---

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://atcoder.jp/contests/yahoo-procon2019-qual/tasks/yahoo_procon2019_qual_e" data-iframely-url="//cdn.iframe.ly/LkBzFTY"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

## 考察

行列に $(0,1)$—ベクトルを掛けていくつかの行・列を取り出すことなどを考えると、問題は次のように言い換えられます。

> $N \times M$ の $\mathbb{F}_2$ 行列 $A$ が与えられる。$vAw=1$ であるような行ベクトル $v \times \mathbb{F}_2^N$ と列ベクトル $w \in \mathbb{F}_2^M$ の組の個数を求めよ。

$vA=0$ の場合、条件を満たす $w$ は明らかに $0$ 個です。$vA\neq0$ の場合には、条件を満たす $w$ は**全体の半分である $2^{M-1}$ 個**になります（$vA$ のある非零成分の位置に対応する $w$ の成分は、それ以外を任意に決めると自動的に定まる）。

$r=\mathrm{rank} A$ とおくと、次元定理より $vA=0$ となる $v$ の個数は $2^{N-r}$ となり、答えは $(2^N-2^{N-r})2^{M-1}$ です。掃き出し法はこの方法が簡単です。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">xor の掃き出しすごい簡単に出来るんですね<br><br>vector&lt;int&gt; basis;<br>for(int e : a){<br> for(int b : basis)<br> chmin(e, e ^ b);<br> if(e)<br> basis.push_back(e);<br>}<br><br>これで数列 a の基底が basis に入る</p>&mdash; 熨斗袋 (@noshi91) <a href="https://twitter.com/noshi91/status/1200702280128856064?ref_src=twsrc%5Etfw">November 30, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## 別解

<iframe src="https://hatenablog-parts.com/embed?url=https%3A%2F%2Fdrken1215.hatenablog.com%2Fentry%2F2019%2F02%2F10%2F024200" style="border: 0; width: 100%; height: 190px;" allowfullscreen scrolling="no"></iframe>

無理やり関連させると、$vAw$ を考える代わりに $(vP^{-1})(PAQ)(Q^{-1}w)$ を考えてもよい、ということになりそう。
