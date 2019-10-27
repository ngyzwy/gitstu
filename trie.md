## 字典树

``` c++
int len, rt, tr[maxn][27], vis[maxn];

void ins()
{
    len = strlen(s);
    rt = 0;
    for (int i = 0; i < len; ++i)
    {
        int to = s[i] - 'a';
        if (!tr[rt][to])
            tr[rt][to] = ++tot;
        rt = tr[rt][to];
    }
    vis[tr[rt][to]]++;
}

int fnd()
{
    int len = strlen(s);
    rt = 0;
    for (int i = 0; i < len; ++i)
    {
        int to = s[i] - 'a';
        if (!tr[rt][to])
            return 0;
        rt = tr[rt][to];
    }
    return vis[rt];
}
```
