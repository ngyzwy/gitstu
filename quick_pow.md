## 快速幂

``` c++
long long quick_pow(long long x, long long y)
{
    long long res = 1;
    while (y)
    {
        if (y & 1)
        {
            res = res * x % mod;
        }
        x = x * x % mod;
        y >>= 1;
    }
    return res;
}
```
