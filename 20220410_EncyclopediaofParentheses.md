# はじめに
AtCoder現在茶色(年内には緑が目標！）のあんこちゃん(@Chunky_RBP_chan)です。
典型問題は抑えとかねばということで、★2〜★5に取り組んでいます。
Pythonで取り組まれている方も多いと思うので自分の解答をシェアしたいと思います！
# 002 Yokan Party

https://atcoder.jp/contests/typical90/tasks/typical90_b

## 解法
"(" → 0
")" → 1
としてbit全探索を考えます。この場合、入力例3は\
3→0011→(()) \
5→0101→()() \
となり辞書順に調べられています。\
また、制約が1<=N<=20なので2^20 ~ 10^6程度となりbit全探索は十分間に合います。\
適切な文字列かは変数count(初期値は0)に対して\
"("は1を足す\
")"は1を引く\
を文字列の左から順に行います。適切な文字列の条件は\
「途中でcountが負にならない」かつ「文字列を調べ終わったときにcount=0」\
でこれらの文字列の数が解答となります。

```python
N = int(input())
for i in range(2**N):
    tmp = ''
    for j in range(N):
        if i & (1<<j) > 0:
            tmp = ')' + tmp
        else:
            tmp = '(' + tmp
    count = 0
    for i in range(N):
        if tmp[i] == '(':
            count += 1
        else:
            count -= 1
        if count < 0:
            break
    else:
        if count == 0:
            print(tmp)
