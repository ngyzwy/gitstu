## 三分

[题目链接：洛谷p3382](https://www.luogu.org/problem/P3382)

``` c++
//洛谷p3382
#include <cstdio>
#include <cmath>
using namespace std;

const double eps = 1e-12;
double l, r, m1, m2, a[15];
int n;

double f (double x)
{
    double sum = 0;
    for (int i = 0, j = n; i <= n; ++i, --j)
    {
        sum = sum + a[i]*pow(x, j);
    }
    return sum;
}

int main ()
{
    scanf("%d %lf %lf", &n, &l, &r);
    for (int i = 0; i <= n; ++i)
    {
        scanf("%lf", &a[i]);
    }
    while (r - l >= eps)
    {
        m1 = l + (r - l) / 3;
        m2 = r - (r - l) / 3;
        if (f(m2) - f(m1) >= eps)
        {
            l = m1;
        }
        else
        {
            r = m2;
        }
    }
    printf("%.5lf\n", l);
    return 0;
}
```
