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

コメント中の `s[..i]` は「入力の上 $i$ 桁」の気持ちです．$X (=10q+r)$ は数え上げる対象です．

```cpp
char s[101]; // 入力
int memo[101][2][4];

// X <= s[..i] もしくは X < s[..i] に対する数え上げ
int f(int i, bool leq, int k) {
  int& ret = memo[i][leq][k];
  if (ret != -1) return ret;

  if (i == 0) {
    // X == 0 のみ
    return ret = (leq && k == 0) ? 1 : 0;
  }

  int ub = s[i - 1] - '0' + leq;

  // q := X / 10, r := X % 10
  // 10 * q + r < 10 * s[..i-1] + ub

  // r < ub のとき q <= s[..i-1]
  // r >= ub のとき q < s[..i-1]

  ret = 0;
  // r == 0
  ret += f(i - 1, 0 < ub, k);
  // 0 < r < ub
  if (k > 0) ret += f(i - 1, true, k - 1) * max(0, ub - 1);
  // ub <= r < 10, r > 0
  if (k > 0) ret += f(i - 1, false, k - 1) * (10 - max(1, ub));
  return ret;
}
```

要するに，$1$ の位だけ見たときに不等式制約に違反していたら，それより上の桁では strict な不等式が成立することが必要で，違反していなければ strict でなくてよいということです．

[提出](https://atcoder.jp/contests/abc154/submissions/25648538)

このメモ化再帰を，ループによってそのまま書き換えてみます．

```cpp
char s[101];
// (i, leq, k): X <= s[..i] もしくは X < s[..i] に対する数え上げ
int dp[101][2][4];

int main() {
  int k;
  scanf("%s%d", s, &k);
  int n = strlen(s);

  dp[0][1][0] = 1;

  rep(i, n) rep(leq, 2) rep(k, 4) {
    int ub = s[i] - '0' + leq;
    int& ans = dp[i + 1][leq][k];

    ans += dp[i][0 < ub][k];
    if (k > 0) ans += dp[i][1][k - 1] * max(0, ub - 1);
    if (k > 0) ans += dp[i][0][k - 1] * min(9, 10 - ub);
  }

  printf("%d\n", dp[n][1][k]);
}
```

[提出](https://atcoder.jp/contests/abc154/submissions/25648538)

ただの貰うDPですね．変数 `leq` が桁DPのいわゆる `tight` フラグに対応していそうです．

[opt さんのブログ](https://opt-cp.com/digit-dp-implementation/) にはこの問題を含めた桁DPの，配るDPによる実装のコツが解説されています．興味深い違いだなと思います．

## ABC129-E Sum Equals Xor

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

```cpp
bitset<64> l, r;
// (i, l_x, y_r, y_2x): (x, y) の数え上げ
// l_x: 数え上げ対象の条件が l <= x か l < x か
// y_r: y <= r か y < r か
// y_2x: y <= 2x か y < 2x か
mint dp[65][2][2][2];

int main() {
  long long li, ri;
  scanf("%lld%lld", &li, &ri);
  l = li, r = ri;

  dp[0][1][1][1] = 1;

  rep(i, 64) rep(l_x, 2) rep(y_r, 2) {
    mint (&ans)[2] = dp[i + 1][l_x][y_r];
    int xlb = l[63 - i] - l_x, yub = r[63 - i] + y_r;

    ans[0] += dp[i][0 > xlb][0 < yub][0];
    ans[1] += dp[i][0 > xlb][0 < yub][1];

    ans[0] += dp[i][0 > xlb][1 < yub][0];
    ans[1] += dp[i][0 > xlb][1 < yub][0];

    ans[0] += dp[i][1 > xlb][1 < yub][1];
    ans[1] += dp[i][1 > xlb][1 < yub][1];
  }

  printf("%d\n", dp[64][1][1][0].val());
}
```

[提出](https://atcoder.jp/contests/abc138/submissions/25649869)
