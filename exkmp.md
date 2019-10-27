## 扩展KMP

>求T的每一个后缀与P的最长公共前缀

>nxt[i]表示p[i...m-1]与p[0...m-1]的最长公共前缀

>extend[i]表示t[i...n-1]与p[0...m-1]的最长公共前缀

>e-kmp:找到i + extend[i] == length(s2)

``` c++
//hdu2594
//kmp也可

#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

const int maxn = 5e4 + 3;
char p[maxn], t[maxn];
int nxt[maxn], extend[maxn];

void pre_ekmp(int m)
{
    nxt[0] = m;
    int j = 0;
    while (j + 1 < m && p[j] == p[j + 1])
        j++;
    nxt[1] = j;
    int k = 1;
    for (int i = 2; i < m; ++i)
    {
        int P = nxt[k] + k - 1;
        int L = nxt[i - k];
        if (i + L < P + 1)
            nxt[i] = L;
        else
        {
            j = max(0, P - i + 1);
            while (i + j < m && p[i + j] == p[j])
                j++;
            nxt[i] = j;
            k = i;
        }
    }
}
//返回t[i...n-1]与p[0...m-1]的最长公共前缀
int ekmp()
{
    int m = strlen(p);
    int n = strlen(t);
    pre_ekmp(m);
    int j = 0, ans = 0;
    while (j < n && j < m && p[j] == t[j])
        j++;
    extend[0] = j;
    int k = 0;
    for (int i = 1; i < n; ++i)
    {
        int P = extend[k] + k - 1;
        int L = nxt[i - k];
        if (i + L < P + 1)
            extend[i] = L;
        else
        {
            j = max(0, P - i + 1);
            while (i + j < n && j < m && p[j] == t[i + j])
                j++;
            extend[i] = j;
            k = i;
        }
    }
    for (int i = 0; i < n; ++i)
        if (ans < extend[i] && extend[i] + i == n)
            ans = extend[i];
    return ans;
}

int main ()
{
    while (~scanf("%s %s", p, t))
    {
        int n = ekmp();
        for (int i = 0; i < n; ++i)
            printf("%c", p[i]);
        if (n)
            printf(" ");
        printf("%d\n", n);
    }
    return 0;
}
```
