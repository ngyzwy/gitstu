## 01字典树

``` c++
int tot, tr[32 * MAXN][2], val[32 * MAXN];

void ins (int x)
{
    int rt = 0;
    for (int i = 31; i >= 0; --i)
    {
        int p = ((x >> i) & 1);
        if (!tr[rt][p])
            tr[rt][p] = ++tot;
        rt = tr[rt][p];
        val[rt]++;
    }
    val[rt] = x;
}

int find_max(int x) //查询所有数中和num异或结果最大的数 
{
    int rt = 0;
    for (int i = 31; i >= 0; --i)
    {
        int p = ((x >> i) & 1);
        if (tr[rt][p ^ 1])
            rt = tr[rt][p ^ 1];
        else
            rt = tr[rt][p];
    }
    return val[rt];
}

int find_min(int x) //查询所有数中和num异或结果最小的数 
{
    int rt = 0;
    for (int i = 31; i >= 0; --i)
    {
        int p = ((x >> i) & 1);
        if (tr[rt][p])
            rt = tr[rt][p];
        else
            rt = tr[rt][p ^ 1];
    }
    return val[rt];
}
```

## 01字典树删除操作

``` c++
int tot, tr[MAXN * 32][2], val[MAXN * 32], vis[MAXN * 32 * 2];

void ins (int x)
{
    int rt = 0;
    for (int i = 30; i >= 0; --i)
    {
        int p = (x >> i) & 1;
        if (!tr[rt][p])
        {
            tr[rt][p] = ++tot;
        }
        rt = tr[rt][p];
        vis[rt]++;
    }
    val[rt] = x;
}

int fnd (int x)
{
    int rt = 0;
    for (int i = 30; i >= 0; --i)
    {
        int p = (x >> i) & 1;
        if (vis[tr[rt][p ^ 1]] > 0 && tr[rt][p ^ 1])
        {
            rt = tr[rt][p ^ 1];
        }
        else if (vis[tr[rt][p]] > 0)
        {
            rt = tr[rt][p];
        }
        else
        {
            return 0;
        }
    }
    return x ^ val[rt];
}

void update(int x, int op)  //op = -1删除这个数op = 1加上这个数 
{
    int rt = 0;
    for (int i = 30; i >= 0; --i)
    {
        rt = tr[rt][(x >> i) & 1];
        vis[rt] += op;
    }
}
```
