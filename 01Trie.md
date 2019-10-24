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
