# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！
# 003 Longest Circular Road
https://atcoder.jp/contests/typical90/tasks/typical90_c

## 解法
最も遠い(間にある街が最も多い)2つの街を見つけ、この2つの街をつなげれば良いです。\
今回の問題ではどの街にも道がつながっており、N個の街に対して道の本数はN−１本であることからこれらの街が作るグラフは木になっています。\
したがって問題は、\
最も遠い2つの街を見つける → 木の直径(最もノードが含まれる経路)を見つける\
と言い換えられます。\
木の直径はBFSを二度行うことで求められ具体的には\
・まず適当なノード(私の場合は0を選びました)からBFSを行い最も遠いノードAを探す。\
・最も遠いノードAからBFSを行い、Aから最も遠いノードBまでの距離を求める。\
最終的に求まったAからBまでの距離が木の直径です。

なぜそうなるか気になる方は

https://qiita.com/nomikura/items/a4c5be6c72ce854d7ce4

をご参考ください。



```python
from collections import deque

def bfs(start):
    Q = deque()
    Q.append(start)
    W = [-1]*N
    W[start] = 0
    while Q:
        now = Q.popleft()
        for i in G[now]:
            if W[i] == -1:
                Q.append(i)
                W[i] = W[now] + 1
    m = max(W)
    for i in range(N):
        if W[i] == m:
            return W,i


N = int(input())
G = [[] for _ in range(N)]
for _ in range(N-1):
    a,b = map(int, input().split())
    G[a-1].append(b-1)
    G[b-1].append(a-1)
W,edge = bfs(0)
W,edge = bfs(edge)
print(W[edge]+1)
