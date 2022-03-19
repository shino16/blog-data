---
title: "1の位で場合分けする桁DP (C++)"
date: 2021-09-06T19:32:00+09:00
tag:
- アルゴリズム
- DP
- 実装
---

## ABC154-E Almost Everywhere Zero

この問題を考えます．素直な桁DPです．

> **問題文**
> $1$ 以上 $N$ 以下の整数であって、$10$ 進法で表したときに、$0$ でない数字がちょうど $K$ 個あるようなものの個数を求めてください。
>
> **制約**
> $1 \leq N < 10^{100}$
> $1 \leq K \leq 3$

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://atcoder.jp/contests/abc154/tasks/abc154_e" data-iframely-url="//cdn.iframe.ly/i8TEMpI"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

この問題について，[maspy さんのHP](https://maspypy.com/atcoder-%e5%8f%82%e5%8a%a0%e6%84%9f%e6%83%b3-2019-02-09abc-154#toc4) では「メモ化再帰」での実装が解説されています．数え上げる対象を $1$ の位で場合分けして，漸化式を作るものです．

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://maspypy.com/atcoder-%e5%8f%82%e5%8a%a0%e6%84%9f%e6%83%b3-2019-02-09abc-154#toc4" data-iframely-url="//cdn.iframe.ly/W296i0g"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

このメモ化再帰を C++ でもやってみます．多倍長整数を使って $\lfloor N/10 \rfloor$ や $\lfloor N/10 \rfloor - 1$ をそのまま持ち回す代わりに，制約を「$X \leq (\text{$N$ の上 $i$ 桁})$」「$X < (\text{$N$ の上 $i$ 桁})$」の形で表現しています．

コメント中の `s[..i]` は「入力の上 $i$ 桁」を表します．$X\\;(=10q+r)$ は数え上げる対象です．

```cpp
char s[101]; // 入力
int memo[101][2][4];

// X <= s[..i] もしくは X < s[..i] に対する数え上げ
int f(int i, bool leq, int k) {
  if (k < 0) return 0;
  int& ret = memo[i][leq][k];
  if (ret != -1) return ret;

  if (i == 0) {
    // X == 0 のみ
    return ret = (leq && k == 0) ? 1 : 0;
  }

  int ub = s[i - 1] - '0' + leq;

  // q := X / 10, r := X % 10
  // 10 * q + r < 10 * s[..i-1] + ub

  ret = 0;
  rep(r, 10) ret += f(i - 1, r < ub, k - (r != 0));
  return ret;
}
```

[提出](https://atcoder.jp/contests/abc154/submissions/27972847)


「$1$ の位だけ見たときに不等式制約を満たしている $\Longleftrightarrow$ それより上の桁では等号付きの不等式が成立すれば十分」と意識すると書きやすいです．

このメモ化再帰を，そのままループに書き換えてみます．

```cpp
char s[101];
// (i, leq, k): X <= s[..i] もしくは X < s[..i] に対する数え上げ
int dp[101][2][4];

int main() {
  int k;
  scanf("%s%d", s, &k);
  int n = strlen(s);

  dp[0][1][0] = 1;

  rep(i, n) rep(leq, 2) rep(k, 4) rep(r, 10) {
    int ub = s[i] - '0' + leq;
    if (k - (r != 0) >= 0)
      dp[i + 1][leq][k] += dp[i][r < ub][k - (r != 0)];
  }

  printf("%d\n", dp[n][1][k]);
}
```

[提出](https://atcoder.jp/contests/abc154/submissions/27972868)

貰うDPであるという点以外はよくある桁DPの実装と同じ形になったと思います．変数 `leq` は桁DPのいわゆる `tight` フラグと役割が似ています．

## ABC129-E Sum Equals Xor

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://atcoder.jp/contests/abc129/tasks/abc129_e" data-iframely-url="//cdn.iframe.ly/api/iframe?url=https%3A%2F%2Fatcoder.jp%2Fcontests%2Fabc129%2Ftasks%2Fabc129_e&key=db98f8c5577d0512bf5cb79a9237e006"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

> $a + b \leq L$ かつ $a + b = a\ \mathrm{XOR}\ b$ なる非負整数の組 $(a, b)$ の個数を求めよ．
>
> $1 \leq L < 2^{100001}$

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://atcoder.jp/contests/abc129/tasks/abc129_e" data-iframely-url="//cdn.iframe.ly/mYTPwcy"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

最初から貰うDPの形で書いてみます．

```cpp
char s[100002];
// (i, leq): a + b <= s[..i] もしくは a + b < s[..i] に対する数え上げ
mint dp[100002][2];

int main() {
  scanf("%s", s);
  int n = strlen(s);

  dp[0][1] = 1;

  rep(i, n) rep(leq, 2) {
    mint& ans = dp[i + 1][leq];
    int ub = s[i] - '0' + leq;
    ans += dp[i][0 + 0 < ub];
    ans += dp[i][0 + 1 < ub] * 2;
  }

  printf("%d\n", dp[n][1].val());
}
```

[提出](https://atcoder.jp/contests/abc129/submissions/25647346)

比較のため，配るDPも書いておきます．

```cpp
char s[100002];
// (i, tight)
mint dp[100002][2];

int main() {
  scanf("%s", s);
  int n = strlen(s);

  dp[0][1] = 1;

  rep(i, n) rep(tight, 2) {
    mint prv = dp[i][tight];
    if (s[i] == '0') {
      // 0, 0
      dp[i + 1][tight] += prv;
      // 0, 1
      if (!tight) dp[i + 1][false] += prv * 2;
    } else {
      // 0, 0
      dp[i + 1][false] += prv;
      // 0, 1
      dp[i + 1][tight] += prv * 2;
    }
  }

  printf("%d\n", (dp[n][0] + dp[n][1]).val());
}
```

[提出](https://atcoder.jp/contests/abc129/submissions/25647828)

## ABC138-F Coincidence （おまけ）

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://atcoder.jp/contests/abc138/tasks/abc138_f" data-iframely-url="//cdn.iframe.ly/api/iframe?url=https%3A%2F%2Fatcoder.jp%2Fcontests%2Fabc138%2Ftasks%2Fabc138_f&key=db98f8c5577d0512bf5cb79a9237e006"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

$L \leq x \leq y \leq R$，$y < 2x$，$\operatorname{bits}(x) \subseteq \operatorname{bits}(y)$ なる $x$，$y$ を数える問題です．

```cpp
bitset<64> l, r;
// (i, l_x, y_r, y_2x): (x, y) の数え上げ
// l_x: 数え上げ対象の条件が l <= x (1) か l < x (0) か
// y_r: y <= r か y < r か
// y_2x: y <= 2x か y < 2x か
mint dp[65][2][2][2];

int main() {
  long long li, ri;
  scanf("%lld%lld", &li, &ri);
  l = li, r = ri;

  dp[0][1][1][1] = 1;

  rep(i, 64) rep(l_x, 2) rep(y_r, 2) {
    int xlb = l[63 - i] - l_x, yub = r[63 - i] + y_r;

    rep(yi, 2) rep(xi, yi + 1) { // y, x の一の位
      dp[i + 1][l_x][y_r][0]
        += dp[i][xi > xlb][yi < yub][yi < xi * 2];
      dp[i + 1][l_x][y_r][1]
        += dp[i][xi > xlb][yi < yub][yi <= xi * 2];
    }
  }

  printf("%d\n", dp[64][1][1][0].val());
}
```

[提出](https://atcoder.jp/contests/abc138/submissions/25649869)
