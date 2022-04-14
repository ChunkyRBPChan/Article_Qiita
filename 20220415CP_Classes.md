# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。\
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。\
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！

# 問題
https://atcoder.jp/contests/typical90/tasks/typical90_g

# 解法
Q人の生徒それぞれのレベルにもっとも合うクラスに分ける問題です。\
二分探索によって生徒iのレーティング$B_i$が$A_j$と$A_{j+1}$の間となるjを見つけます。jがわかれば$|B_i-A_j|$と$|B_i-A_{j+1}|$の小さい方が答えとなります。\
注意として、j=-1の場合とj=Nの場合$A_j$もしくは$A_{j+1}$がないので別処理が必要です。

```python
def bisect(X):
    right = N
    left = -1
    while right-left>1:
        mid = (right+left)//2
        if X < A[mid]:
            right = mid
        else:
            left = mid
    if left == -1:
        return A[right]-X
    if right == N:
        return X-A[left]
    return min(abs(A[left]-X),abs(A[right]-X))

N = int(input())
A = list(map(int, input().split()))
A.sort()
Q = int(input())
for _ in range(Q):
    b = int(input())
    print(bisect(b))
