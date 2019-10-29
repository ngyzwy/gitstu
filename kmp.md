## KMP

``` c++
void get_nxt() //获取next数组 
{
    int i = 0, j;
    j = nxt[0] = -1;
    while (i < m) //m为模式串长度 
    {
        if (-1 == j || p[i] == p[j]) //p为模式串 
        {
            i++;
            j++;
            nxt[i] = j;
        }
        else
        {
            j = nxt[j];
        }
    }
}

int kmp() //返回模式串在主串出现的次数 
{
    get_nxt();
    int i = 0, j = 0, cnt = 0;
    while (i < n) //n为主串长度 
    {
        if (-1 == j || t[i] == p[j])
        {
            i++;
            j++;
        }
        else
        {
            j = nxt[j];
        }
        if (j >= m)
        {
            cnt++; //匹配成功 
        }
    }
    return cnt;
}
```
