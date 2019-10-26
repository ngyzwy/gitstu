## 01背包

>n件物品，背包容量W
>第i件物品重量w[i]价值v[i]

``` c++
//无优化 
for (int i = 1; i <= n; ++i)
    for (int j = 0; j <= W; ++j)
        if (j < w[i])
            dp[i][j] = dp[i - 1][j];
        else
            dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - w[i]] + v[i]);
    
//一维数组优化
for (int i = 1; i <= n; ++i)
    for (int j = W; j >= w[i]; --j)
        dp[j] = max(dp[j], dp[j - w[i]] + v[i]);

//更进一步的常数优化
for (int i = 1; i <= n; ++i)
{
    sumw += w[i];
    t = max(W - sumw, w[i]);
    for (int j = W; j >= t; --j)
        dp[j] = max(dp[j], dp[j - w[i]] + v[i]);
}

//不要求把背包装满，只希望价格尽量大，初始化dp[0...V]全为0
//恰好装满背包，初始化除了dp[0]为0其它dp[1...V]均初始化为-∞
```

## 完全背包

``` c++
for (int i = 1; i <= n; ++i)
    for (int j = w[i]; j <= W; ++j)
        dp[j] = max(dp[j], dp[j - w[i] + v[i]]);
```

## 多重背包

``` c++
//代码未经测试
for(int i=1;i<=n;i++)
{
    if(w[i]*a[i]>m)
    {
        for(int c=0;c<=m;c++)
        {
        if(c>=w[i])
        f[c]=max(f[c],f[c-w[i]]+v[i]);
        }
    }
    else
    {
         k=1;amount=a[i];
         while(k<amount)
         {
             for(int c=k*w[i];c>=0;c--)
             {
                 if(c>=w[i])
                 f[c]=max(f[c],f[c-w[i]]+k*v[i]);
             }
             amount-=k;
             k<<=1;
         }  
         for(int c=amount*w[i];c>=0;c--)
         {
             f[c]=max(f[c],f[c-w[i]]+amount*v[i]);
         }
    } 
}
```

## 背包伪代码

``` c++
//01背包 C空间W价值
def ZeroOnePack(F, C, W)
    for v = V to C
        F[v] = max(F[v], F[v - C) + W)

//完全背包
def CompletePack(F, C, W)
    for v = C to V
        F[v] = max(F[v], F[v - C] + W)

//多重背包 每个物品M件可选
def MultiplePack(F, C, W, M)
    if C * M >= V
        CompletePack(F, C, W)
        return
    k := 1
    while k < M
        ZeroOnePack(kC, kW)
        M := M - k
        k := 2k
    ZeroOnePack(C * M, W * M)
```
