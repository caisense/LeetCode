# DP总结

其实就两点：状态（dp数组）和选择（min，max求最值）

0/1背包
定义：物品只能用一次

`dp[i][j] = max(dp[i-1][j], dp[i-1][j-weight[i]] + value[i])`

