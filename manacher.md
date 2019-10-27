## 马拉车

``` c++
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

const int maxn = 99;
int Mp[maxn * 2];
char s[maxn], Ma[maxn * 2];

void Manacher()
{
    int l = 0;
    Ma[l++] = '$';
    Ma[l++] = '#';
    for (int i = 0; s[i]; ++i)
    {
        Ma[l++] = s[i];
        Ma[l++] = '#';
    }
    Ma[l] = 0;
    int mx = 0, id = 0;
    for (int i = 0; i < l; ++i)
    {
        Mp[i] = mx > i ? min(Mp[2 * id - i], mx - i) : 1;
        while (Ma[i + Mp[i]] == Ma[i - Mp[i]])
            Mp[i] ++;
        if (i + Mp[i] > mx)
        {
            mx = i + Mp[i];
            id = i;
        }
    }
}

int main ()
{
    int len, ans = 0;
    scanf("%s", s);
    len = strlen(s);
    Manacher();
    for (int i = 0; i < 2 * len + 2; ++i)
        ans = max(ans, Mp[i] - 1);
    printf("%d\n", ans);
    return 0;
}
/*
input:
 
abaaba

output:

6
*/
```
