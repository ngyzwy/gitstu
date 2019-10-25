## 前缀和

``` c++
int a[MAXN];
for (int i = 1; i <= n; ++i)
{
    scanf("%d", &a[i]);
    a[i] = a[i] + a[i - 1];
}
```

## 二维前缀和

``` c++
int a[MAXN][MAXN];
for (int i = 1; i <= n; ++i)
{
    for (int j = 1; j <= m; ++j)
    {
        scanf("%d", &a[i][j]);
        a[i][j] += a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1];
    }
}
```
