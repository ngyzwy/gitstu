## 最大公约数

``` c++
//递归实现
int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}

//非递归实现
int gcd(int a, int b)
{
    int r;
    while (b)
    {
        r = b;
        b = a % b;
        a = r;
    }
    return a;
}
```
