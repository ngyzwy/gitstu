## 二维RMQ

``` c++
const int inf = 0x3f3f3f3f; 
const int MAXN = 103;
int dp_min[MAXN][MAXN][29], dp_max[MAXN][MAXN][29];;

void st(int n) //预处理
{
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            scanf("%d", &dp_min[i][j][0]);
            dp_max[i][j][0] = dp_min[i][j][0];
        }
    }
    for (int k = 1; k <= n; ++k)
    {
        for (int j = 1; (1 << j) <= n; ++j)
        {
            for (int i = 1; i + (1 << j) - 1 <= n; ++i)
            {
                dp_min[k][i][j] = min(dp_min[k][i][j - 1], dp_min[k][i + (1 << (j - 1))][j - 1]);
                dp_max[k][i][j] = min(dp_max[k][i][j - 1], dp_max[k][i + (1 << (j - 1))][j - 1]);
            }
        }
    }
}

int rmq(int x, int y, int len) //查询 
{
    int k = log2(len), maxx = -inf, minn = inf;
    for (int i = x; i < x + len; ++i)
    {
        maxx = max(maxx, max(dp_max[i][y][k], dp_max[i][(y + b - 1) - (1 << k) + 1][k]));
        minn = max(minn, min(dp_min[i][y][k], dp_min[i][(y + b - 1) - (1 << k) + 1][k]));
    }
    return maxx - minn;
}
```
