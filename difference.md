## 差分

``` c++
int a[N] = {0};  //差分数组
for (int i = 1; i <= t; ++i) //区间t次操作
{
    scanf("%d %d", &x, &y);  //也可以区间改变值为v
    a[x]++;
    a[y + 1]--;
}
for (int i = 1; i <= n; ++i)
{
    a[i] += a[i - 1];
    printf("%d ", a[i]);
}
```

## 二维差分

``` c++
int a[N + 1][M + 1] = {0};   //差分数组
for (int i = 1; i <= t; ++i) //区间t次操作
{
    scanf("%d %d %d %d", &x1, &y1, &x2, &y2); //也可以区间改变值为v
    a[x1][y1]++;
    a[x2 + 1][y2 + 1]++;
    a[x2 + 1][y1]--;
    a[x1][y2 + 1]--;
}
for (int i = 1; i <= n; ++i)
{
    for (int j = 1; j <= m; ++j)
    {
        a[i][j] += a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1];
        printf("%d ", a[i][j]);
    }
    printf("\n");
}
```
