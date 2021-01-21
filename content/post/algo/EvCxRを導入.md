---
title: "EvCxRを導入"
date: 2020-11-03T17:00:10+09:00
draft: true
tag:
- 環境構築
---

[EvCxR](https://github.com/google/evcxr) を Windows 環境にインストールしました。うまく行ったことや行かなかったことの記録です。

[Jupyter Kernel](https://github.com/google/evcxr/blob/master/evcxr_jupyter/README.md) が欲しかったんですが、なんだかうまくいかず、諦めて CI だけの [REPL](https://github.com/google/evcxr/blob/master/evcxr_repl/README.md) を導入しました。

## EvCxR とは

REPL というやつで、式を打ち込むと実行してくれるものです。

<iframe src="https://hatenablog-parts.com/embed?url=https%3A%2F%2Fqnighy.hatenablog.com%2Fentry%2F2018%2F09%2F29%2F190000" style="border: 0; width: 100%; height: 190px;" allowfullscreen scrolling="no"></iframe>

競プロや Project Euler 用に、手早く計算したり実験できる環境がほしくて、Jupyter の Rust 版みたいなのないかなと思ったら [あった](https://github.com/google/evcxr/blob/master/evcxr_jupyter/README.md) というのがきっかけ。

"evcxr is currently the best REPL implementation" ([https://github.com/rust-lang/rust/issues/1120#issuecomment-626317169](https://github.com/rust-lang/rust/issues/1120#issuecomment-626317169)) とのことです。[papyrus](https://github.com/kurtlawrence/papyrus) というのもありましたが、いまいち手元でうまく動かなかいっぽく、開発も終了していました。

## 導入の流れ

[EvCxR Jupyter Kernel](https://github.com/google/evcxr/blob/master/evcxr_jupyter/README.md) を入れようとしましたが、`cargo install` が [ZMQ](https://github.com/zeromq/libzmq) なるもののインストールに失敗しているらしい。

[README の記述](https://github.com/google/evcxr/blob/master/evcxr_jupyter/README.md#windows) に従って先に [ZMQ](https://github.com/zeromq/libzmq) を Visual Studio でビルドしてもいいらしいですが、そこまではしませんでした。バイナリで配布してくれたら楽なんですが…

Jupyter Kernel がない方の [REPL](https://github.com/google/evcxr/blob/master/evcxr_repl/README.md) を試しました。インストール・起動はできたものの、何か実行するとエラーになりました。

GitHub の `master` ブランチを取ってきて `cargo install --path evcxr/evcxr_repl` みたいなことをするとうまく行きました。

## 使用感

※ Jupyter 版もそうでない方もバックグラウンドで動いているものは同じなので、だいたいのことは共通しているはず

### できること

式の評価、変数・関数・型etc.の定義、ローカル・`crates.io`上のクレートの利用、時間計測、など

* 式の評価

* 変数・関数・型etc.の定義

行（実行単位）をまたがって持ち越されます。

* クレートの利用

`Cargo.toml` に書くときのように、`:dep rand = "0.7"` とか `:dep library = { path = "/aboslute/path/to/library" }` みたいなことを書くと依存関係も含めてビルドしてくれて、次の行からは使えるようになっていました。

ローカルのクレートについては、各行の実行ごとに手元で書き換えたものがすぐに反映されます。過去に使用した関数を削除するとさかのぼって怒られたりした。ライブラリのちょっとした確認に便利そう。

`crates.io` のものは行ごとにコンパイルはされないけど EvCxR を再起動するとコンパイルし直しになるようです。ものによってはそれなりの時間がかかります。

* 時間計測

`:timing` と打つと、行ごとに実行時間を報告してくれます。

### 速度について

`1+1` みたいなのでも、だいたいのものが実行に２～３秒かかります。（けっこうすごいことをしているらしい　[RustのREPL "evcxr" を使ってみた - 簡潔なQ](https://qnighy.hatenablog.com/entry/2018/09/29/190000) の「仕組み」の部分）

Jupyter Kernel の README にはこんな記述があったので、Windows 固有かもしれません。

> Note that Evcxr on Windows appears to be substantially slower than on other platforms. We're not yet sure why.

と言いながらこんな issue もあり、どの環境でもそこまで変わらないんじゃないかという気も？

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://github.com/google/evcxr/issues/52" data-iframely-url="//cdn.iframe.ly/uXvCACy"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

## メモ

`cargo` のサブコマンドって割とこんな感じだと思うんですが、例えば `stable` toolchain が有効化されたディレクトリで `cargo install` したとき、`1.42.0` が動く競プロ用ディレクトリではうまく実行されないようです。カレントディレクトリを移動すれば直ります。
