## 扩展欧几里得

``` c++
//gcd(a, b) = d = xa + yb 返回d, x, y 
int exgcd(int a, int b, int &x, int &y)
{
    if (a == 0 && b == 0) //无最大公约数 
        return -1;
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    return d;
}
```
