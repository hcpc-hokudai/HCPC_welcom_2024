---
marp: true

theme: beamer
footer: "HCPC 新歓 計算量について"
math: mathjax
style: |
    section.title {
        justify-content: center;
        text-align: left;
    }
    section {
        justify-content: start;
    }
    section::after {
      content: attr(data-marpit-pagination) " / " attr(data-marpit-pagination-total);
    }
---
<!-- _class: title -->
# 計算量について


---

# 計算量とは

<br>


→この解法で問題を解くと、どのくらいの時間で計算し終わるか？という指標

<br>

競プロの問題では、大抵の場合**時間制限** (1~2秒が相場) があって、
「その時間以内にプログラムを終わらせてね〜」という制約がついている。

<br>

あまりにも時間がかかる解法だと、TLE (Time Limit Exceeded) となってしまう。

<br>

**計算量の見積もりが必要！**

---

# ランダウの $O$ 記法

<br>

プログラムの計算量を大雑把に見積もるための指標

$O(X)$ と書いて、「 $X$ 回に比例した回数の計算で終わる」ということを表す。

<br>

```py
N = int(input())
A = list(map(int, input().split()))

S = 0
for i in range(N):
    S += A[i]
```

<br>

ループを回して $N$ 回の計算をしているので、 $O(N)$

---

# ランダウの $O$ 記法

<br>


```py
N = int(input())
A = list(map(int, input().split()))

S = 0
for i in range(N):
    S += A[i]

S2 = 0
for i in range(N):
    S2 += A[i] * A[i]
```

<br>

2回ループを回しているので計算回数は $2N$ 回だが、 $N$ の**定数倍**なので $O(N)$


3回、4回,... でも定数倍は無視して $O(N)$ ( $O$ は大雑把の $O$ )

---

# 色々な計算量

<br>

Q. 配列 $A$ と $B$ が与えられる。$A_1 \times B_1 + A_1 \times B_2 + \cdots + A_N \times B_N$ を計算せよ。


```py
N = int(input())
A = list(map(int, input().split()))
B = list(map(int, input().split()))

S = 0
for i in range(N):
    for j in range(N):
        S += A[i] * B[j]

print(S)
```

<br>

$N$ 回のループの中でさらに $N$ 回のループを回しているので、計算回数は $N^2$ 回
→　$O(N^2)$

---

# 色々な計算量

<br>

Q. 整数 $N$ が与えられる。$1+2+3+\cdots+N$ を計算せよ。



<br>

```py
N = int(input())

S = N * (N + 1) // 2
```

<br>

計算量は $O(1)$


---

# 色々な計算量

<br>

```py
N = int(input())

S = 0
for i in range(0, N):
    for j in range(0, N):
        S += i + j

for i in range(N):
    S += i
```

<br>

計算回数は $N^2 + N$ 回だが、小さい方の $N$ は無視して**大雑把**に表す

→ $O(N^2)$

<br>

一番大きな項以外は全部無視！

---

# 計算量を使って実行時間を見積もる

<br>

競プロの問題では

- $1 \leq N \leq 10^5$
- $0 \leq A_i \leq 10^9$

などの制約が必ず書いてあるので、見積もった計算量に制約の最大値を代入してみる。


→ $10^7$ から $10^8$ くらいに収まれば大体 OK

--- 

# よく見る計算量と限界値

<br>

<br>

| 計算量 | 限界値 |
| --- | --- |
| $O(2^N)$ | $N \leq 20$ |
| $O(N^2)$ | $N \leq 10^4$ くらい |
| $O(N \log N)$ | $N \leq 10^6$ くらい |
| $O(N)$ | $N \leq 10^7$ くらい |
| $O(\log N)$ | $N \leq 10^{18}$ くらい |
| $O(1)$ | なんでも OK |



