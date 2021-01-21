---
title: IOライブラリの設計
date: 2020-10-18 00:00:00 +0900
tags:
- アルゴリズム
- 実装
---

競プロ用の入出力ライブラリ（Rust）を作る

## 要件

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">長年抱えてる葛藤が、貼る用のライブラリをゴテゴテに作りこむか、簡潔にとどめたほうが綺麗かという</p>&mdash; しの (@shino_skycrew) <a href="https://twitter.com/shino_skycrew/status/1313166416242077696?ref_src=twsrc%5Etfw">October 5, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

妥協ラインとして、ライブラリは多少長くしてもよい代わりにすべて `main` 等の下に追いやります。

1. マクロは使わずに、`proconio` の `input!` くらい使いやすいものにしたい
2. おおよそ 100 ms 単位で最速になってほしい

外部クレートには依存しません。（使えるものなら `proconio` を使う…）

## 完成

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://github.com/shino16/cpr/blob/master/src/io.rs" data-iframely-url="//cdn.iframe.ly/htbZ49Y"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

## 使用例

[#27339 – Library-Checker](https://judge.yosupo.jp/submission/27339)（Point Add Range Sum）

下のコードを[なんとかかんとか](https://github.com/shino16/cargo-auto-bundle)で pack? bundle? したもの。

```rust
use lib::io::*;
use lib::ds::fenwick::*;

fn main() {
    let mut io = IO::new();
    let (n, q) = io.scan();
    let a = io.scan_vec(n);
    let mut rsq = Fenwick::new(a, GroupImpl(0, |a, b| a + b, |a: i64| -a));
    for _ in 0..q {
        if io.scan::<u32>() == 0 {
            rsq.add(io.scan(), io.scan());
        } else {
            let res = rsq.ask(io.scan(), io.scan());
            io.println(res);
        }
    }
}
```

とても快適です、ありがとう

純粋に IO の速度を測るなら、[Many A + B](https://judge.yosupo.jp/problem/many_aplusb) を使うべきでしょう。

## 設計

* 初期化時に入力をすべて受け取って `Box::leak` する（これどうなの？）
  * ライフタイムであ"～ってなった時、とりあえずこうすると楽になる
* 出力は `std::io::BufWriter`（この 2 つだけで `tie`/`sync` を切った `cin/cout` や `scanf/printf` より既に速い）
* `scan` が返せる型を `Scan` トレイトで表現し、多相にする
  * ネストしたタプルや配列も空気を読んでやってくれる
  * 整数は `str::parese` の代わりに自力で読む
* `print` が受け取れる値を `Print`（以下略）
  * ネストしたタプルも
* `char`？ 知らない子ですね

## いまいちな点

* 入力を丸ごと `leak` していますが
  * どれくらい良くないのかすらわかりません、気が咎める
  * 高々 $10^5$ 程度のオーダーということで…
* 入力と出力は分離するべきじゃないの？
  * 実際互いに完全に独立している
  * 別オブジェクトだとめんどくさいだけ
* `Scan::scan` や `Print::print` が `&mut IO` を受け取る必要はないのでは？
  * `f: &mut F where F: FnMut() -> &[u8]` とかいちいち書くのも面倒
* インタラクティブは？
  * [`src/io_interactive.rs`](https://github.com/shino16/cpr/blob/master/src/io_interactive.rs) を作りました。適宜 1 行ずつ読み取るという違いだけの、コピペです（悲しい）
  * とはいえ一度に使うのは片方だけだし、いいかな…
* `IO::scan` に、どういうときに型引数を明示的に渡さないといけないのかよくわからない
  * とりあえず怒られてから直す
