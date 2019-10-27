## RMQ

``` c++
const int MAXN = 1e5 + 3;
int dp[MAXN][29];

void st(int n) //预处理n个元素
{
    for (int i = 1; i <= n; ++i)
        scanf("%d", &dp[i][0]);
    for (int j = 1; (1 << j) <= n; ++j)
        for (int i = 1; i + (1 << j) - 1 <= n; ++i)
            dp[i][j] = max(dp[i][j - 1], dp[i + (1 << (j - 1))][j - 1]);
}

int rmq(int l, int r) //查询区间最值
{
    int k = log2(double(r - l + 1));
    return max(dp[l][k], dp[r - (1 << k) + 1][k]);
}
```
