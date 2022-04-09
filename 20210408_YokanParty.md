# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！
# 001 Yokan Party 
https://atcoder.jp/contests/typical90/tasks/typical90_a

## 解法
https://github.com/E869120/kyopro_educational_90/blob/main/editorial/001.jpg

解法については出題者E869120(@e869120)の説明が非常にわかりやすかったので、この解法通り実装します。
簡単な説明としては、

①最小の長さを決め、何個に分割できるか確かめる
②K+1個より多く分割できれば最小の長さを大きくする。K+1より少なければ最小の長さを小さくする。

これを二分探索によって実装します。
K+1個に分割可能な数a,b,c(a <= b <= c)があった場合にcが選ばれるようokを左端にしています。また、ok,ngを変更するif文の不等号に注意しましょう。

```python
N,L = map(int, input().split())
K = int(input())
A = list(map(int,input().split()))
A.append(L)
ok = -1
ng = L
while abs(ok-ng) > 1:
    mid = (ok+ng)//2
    slice = 0
    pre = 0
    for i in A:
        if i-pre >= mid:
            slice += 1
            pre = i
    if slice > K:
        ok = mid
    else:
        ng = mid
print(ok)
