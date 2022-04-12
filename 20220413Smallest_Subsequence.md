# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。\
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。\
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！

# 問題
https://atcoder.jp/contests/typical90/tasks/typical90_f

# 解法
入力\
N K\
S\
に対して、まずN-K文字目までをheappushし、その後N文字目まで次の操作を繰り返すことで答えが得られます。\

**操作**
①N-(K-1)<=i<=Nを満たすiに対して、各iごとにSのi文字目をheappushする。\
②以前でた文字より右にあるものが取り出されるまでheappopし続ける。\
③取り出された文字を以前出た文字の右に付け加える。


## なぜうまくいくか
$N=5、K=3、S=a_1a_2a_3a_4a_5$のとき\
答えの文字列が$b_1b_2b_3$とすると\
$b_1$は必ず$a_1、a_2、a_3$の中にあります。なぜなら$b_1=a_4$であれば$b_2=a_5$であり、$b_3$は存在しなくなるからです。\
今$b_1=a_2$だとすると$b_2$は$a_2$より右側にある辞書順が早い文字なので$a_3、a_4$のどちらかです。\
しかし、$b_2$を選ぶ前heapqには$a_1、a_3、a_4$が入っているため、$a_1$が出た場合はもう一度heappopすれば$a_3、a_4$から$b_2$を選べます。\
以上から、\
①N-(K-1)<=i<=Nを満たすiに対して、各iごとにSのi文字目をheappushする。\
②以前でた文字より右にあるものが取り出されるまでheappopし続ける。\
③取り出された文字を以前出た文字の右に付け加える。\
の操作を繰り返すことで答えの文字列が得られます。



```python
import heapq

N,K = map(int, input().split())
S = input()
Q = []
for i in range(N-K):
    heapq.heappush(Q,(S[i],i))
pre_ind = -1
ans = ''
for i in range(N-K,N):
    heapq.heappush(Q,(S[i],i))
    while True:
        st,ind = heapq.heappop(Q)
        if ind > pre_ind:
            ans = ans + st
            pre_ind = ind
            break
print(ans)
