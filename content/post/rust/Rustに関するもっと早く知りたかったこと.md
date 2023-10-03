---
title: "Rustに関するもっと早く知りたかったこと"
date: 2021-02-02T05:09:57+09:00
draft: true
---

## クロージャの再帰

```rs
struct Recurse<F>(F);
impl<F> Recurse<F> {
    fn call<Arg, Ret>(&self, arg: Arg) -> Ret
    where
        F: Fn(&dyn Fn(Arg) -> Ret, Arg) -> Ret,
    {
        self.0(&|arg| self.call(arg), arg)
    }
}

fn recurse<Arg, Ret, F: Fn(&dyn Fn(Arg) -> Ret, Arg) -> Ret>(f: F) -> Recurse<F> {
    Recurse(f)
}

let rec = recurse(|fib, n: u32| if n <= 1 { 1 } else { fib(n - 1) + fib(n - 2) });
assert_eq!(rec(18), 2584);
```

`dyn` のオーバーヘッドが気になるかもしれないが、この場合ではうまくmonomorphizeしてくれるらしく、普通の再帰関数として書いた場合との性能の差は無い（`cargo bench` で確認した）。上のコードで `Recurse` の中身を `&dyn Fn(&dyn Fn(Arg) -> Ret, Arg) -> Ret` とかにすると、外側はmonomorphizeされず３～４倍の時間がかかった。

`recurse` に渡せるのは `Fn` なので、ミュータブルなキャプチャはできない（`RefCell<T>` を使えばよい）。`RefCell<HashMap<K, V>>` を `Recurse` に持たせればメモ化もできる。

## `static mut` は何が安全でないのか

[https://qiita.com/qnighy/items/46dbf8d2aff7c2531f4e](https://qiita.com/qnighy/items/46dbf8d2aff7c2531f4e)

[https://github.com/rust-lang/rust/issues/53639](https://github.com/rust-lang/rust/issues/53639)

`static mut` はどういう使い方をすると未定義動作になるのか、未だによくわかっていない

`static mut` は Rust の "shared XOR mutable" というエイリアシング規則に簡単に違反できてしまう。場所がグローバルでなくても、いかなる瞬間もメモリ上に `&mut` が複数存在することがないよう、`rustc` の代わりに気をつけなくてはいけない。


## `#[macro_export]` 属性がついたマクロは後方参照できる

使う場所の前方で定義する必要がない

## `RefCell` のオーバーヘッドは無視して良い

`RefCell` を `UnsafeCell` で置き換えても、実行時間は数％しか変わらないがち。
