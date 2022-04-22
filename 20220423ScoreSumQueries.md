# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。\
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。\
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！

# 問題
https://atcoder.jp/contests/typical90/tasks/typical90_j

# 解法
学籍番号ごとに各組の累積和を持っておきます。\
あとは各jについて(R_jまでの和)-(L_jまでの和)を行えばよいです。


```python
N = int(input())
Point = [[0]*(N+1) for _ in range(2)]
for i in range(N):
    c,p = map(int, input().split())
    Point[c-1][i+1] = Point[c-1][i]+p
    if c == 2:
        Point[0][i+1] = Point[0][i]
    else:
        Point[1][i+1] = Point[1][i]
Q = int(input())
for _ in range(Q):
    l,r = map(int, input().split())
    print(Point[0][r]-Point[0][l-1],Point[1][r]-Point[1][l-1])
