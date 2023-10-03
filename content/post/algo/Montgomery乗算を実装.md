---
title: "Montgomery 乗算を実装した"
date: 2020-11-03T23:45:00+0900
tag:
- ライブラリ
---

modulo 演算の高速化です。

<iframe src="https://hatenablog-parts.com/embed?url=https%3A%2F%2Fmin-25.hatenablog.com%2Fentry%2F2017%2F08%2F20%2F171214" style="border: 0; width: 100%; height: 190px;" allowfullscreen scrolling="no"></iframe>

これらのうち、Montgomery 乗算というものを実装しました。

## 余談？　経緯？

Codeforces では C++ 以外 32bit 環境なんだよなとふと思って、演算にどれだけの差が出るのか調べてみました。

どうやら 32bit 環境での 64bit 整数同士の乗算・除算は特に遅いらしい。

> ![画像](https://www.passmark.com/images/forumimages/64bit_vs_32bit_benchmark_V7.png)
>
> 引用：[https://forums.passmark.com/performancetest/3383-64bit-vs-32bit-benchmarks-integer-maths-pt8#post3383](https://forums.passmark.com/performancetest/3383-64bit-vs-32bit-benchmarks-integer-maths-pt8#post3383)

## Montgomery 乗算とは

中国剰余定理の応用みたいなもので、例えば奇数 $M$ に対して、$\bmod M$ の演算を「`% M`」の代わりに $2$ の冪による除算・剰余算（bit 演算）で済ませることができます。$M < 2^{31} = 2147483648$ なら 32bit 整数でうまい感じにできます。

こちらを参考にしました。これらが完璧すぎるので自分は書くことがありません。

[モンゴメリ乗算 Wiki - yukicoder](https://yukicoder.me/wiki/%E3%83%A2%E3%83%B3%E3%82%B4%E3%83%A1%E3%83%AA%E4%B9%97%E7%AE%97)

[モンゴメリ乗算 - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%A2%E3%83%B3%E3%82%B4%E3%83%A1%E3%83%AA%E4%B9%97%E7%AE%97)

というか「modulo 演算の速度差が問題になるようなコンテストに出ない！(素振り)」案件なんですよね。AtCoder や Library Checker では有意な差すら確認できていないのですが（ベンチマークになる問題があれば教えてください）、Codeforces で NTT を投げてみたらこんなことがあり

[Submission #97560132 - Codeforces](https://codeforces.com/contest/954/submission/97560132) TLE (>4000 ms)

[Submission #97563421 - Codeforces](https://codeforces.com/contest/954/submission/97563421) AC (2262 ms)

`main` 関数の中身は同じです。さすがにおかしくないか？ 32bit だと $2^{30}$ 程度の定数による除算・剰余算があまり最適化されなかったりするんでしょうか。

## 実装

yukicoder Wiki、Wikipedia の内容をそのまま実装します。法は奇数であればよいですが、素数と仮定することにします。

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://github.com/shino16/cpr/blob/master/src/fp.rs" data-iframely-url="//cdn.iframe.ly/ZfhHqXV"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

せっかくこういうことをするのに ACL の `dynamic_modint` みたいなのを提供しないのはもったいないんですが、`Mod` の値を `const` にしたいので切りました。
