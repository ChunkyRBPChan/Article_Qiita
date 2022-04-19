# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。\
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。\
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！

# 問題
https://atcoder.jp/contests/typical90/tasks/typical90_h

# 解法
![AtCounter.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/603082/cedf92b4-6d2d-2537-a9a9-4dd78a91c490.png)
DP[i][j]:Sのj-1文字目までにatcoderの1からi-1文字までが含まれる個数となるDPを考えます。

更新式は\
**atcoder[i]=S[j]の時**\
DP[i+1][j+1] += DP[i][j]\
DP[i][j+1] += DP[i][j]\
**atcoder[i] != S[j]の時**\
DP[i][j+1] += DP[i][j]\

例えば、DP[0][0]からDP[1][1]への遷移は\
attcorderの１文字目のaをatcoderのaに選ぶことと同じ意味です。\
一方でDP[0][0]からDP[0][1]への遷移は\
attcoderの1文字目のaを選ばずにattcoderの2文字目への移動を意味します。\
他にもDP[1][1]からDP[2][2]への遷移は\
attcoderの二文字目のtをatcoderのtに選ぶことと同じです。\
したがって、DP[8]にSに含まれるatcoderの個数が並ぶためDP[8]の合計値が答えとなります。


```python
N = int(input())
S = input()
atcoder = 'atcoder'
MOD = 10**9+7
dp = [[0]*8 for _ in range(N+1)]
dp[0][0] = 1
for i in range(N):
    s = S[i]
    for j in range(7):
        if s == atcoder[j]:
            dp[i+1][j+1] += dp[i][j]%MOD
        dp[i+1][j] += dp[i][j]%MOD
    dp[i+1][-1] += dp[i][-1]%MOD
print(dp[-1][-1]%MOD)
