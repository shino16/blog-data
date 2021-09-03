---
title: "AGC041 C - Domino Quality"
date: 2021-03-01T14:38:44+09:00
draft: true
categories:
- "問題"
tags:
- "問題"
- "構築"
---

小さな構成単位を用意して、うまく並べるような方針が浮かびます。例えば、
```
N=3    N=4
aa.    aacd
..a    bbcd
..a    cdaa
       cdbb
```
これを敷き詰めれば、$N$ が $3$ あるいは $4$ の倍数の場合について解くことができます。

$N=7$ の場合は少し困ります。左上に $4\times4$、右下に $3\times3$ を配置しても、二者の各行・列のクオリティが異なるので不適切です。言い換えると、小さな $N$ に対する構成結果を対角線上に並べるとき、それらのクオリティがすべて一致していればよいです。

クオリティはどの値にそろえればよいでしょうか。ドミノを $1$ つ追加するとき、各行・列のクオリティの総和は $3$ だけ増加します。ゆえに各行・列のクオリティの総和はつねに $3$ の倍数です。となると、各クオリティを $3$ にそろえれば良さそうです。上の $N=4$ の構成もそうなっていました。

以下が手で構成した結果です。クオリティが $3$ であることが分かっているので、てきとーにやっているとうまくいきます。

```
N=5       N=7
aabba     a..aabb
bcc.a     a..bbaa
b..cb     bab....
a..cb     bab....
abbaa     aba....
          aba....
          .ccaabb
```

$4\cdot5-(4+5)+1=12$ 以上の整数は $4x+5y$（$x,y$ は整数）の形で表すことができるので、$N=4,5$ の場合の構成を対角線上に並べて構成できます。$3, 6$ は $N=3$ の構成を組み合わせて、$7, 11$ は $N=4,7$ の構成を組み合わせればOKです。$N=2$ はサンプルにもある通り構成できません。

公式解説に載っている $N=7$ の構成は $N=3$ の場合のものをベースにしているようです。$N=6$ も $N=4$ を適当に組み替えているような感じで面白い。

うまく探索して $N \leq 7$ のケースを構築することもできるようです。

<iframe src="https://hatenablog-parts.com/embed?url=https%3A%2F%2Fkenkoooo.hatenablog.com%2Fentry%2F2019%2F12%2F29%2F110321" style="border: 0; width: 100%; height: 190px;" allowfullscreen scrolling="no"></iframe>

公式解説には「乱択で見つけられる」というようなことが書いてありますが、分からず。