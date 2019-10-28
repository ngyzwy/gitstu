## 逆元

``` c++
//ax ≡ 1 (mod n)
long long mod_reverse(long long a, long long n)
{
    long long x, y;
    long long d = exgcd(a, n, x, y);
    if (d == 1)
        return (x % n + n) % n;
    else
        return -1;
}
```
