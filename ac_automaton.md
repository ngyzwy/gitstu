## AC自动机

``` c++
char s[99];
const int maxn = 1e5 + 3;
int index, trie[maxn][26], fail[maxn], num[maxn], slen[maxn];

void insert()
{
    int len = strlen(s), rt = 0;
    for (int i = 0; i < len; ++i)
    {
        int v = s[i] - 'a';
        if (!trie[rt][v])
            trie[rt][v] = ++index;
        rt = trie[rt][v];
    }
    num[rt]++;
    slen[rt] = len; //记录模式串的长度 
}

void build()
{
    queue <int> que;
    for (int i = 0; i < 26; ++i)
        if (trie[0][i])
            que.push(trie[0][i]);
    while (!que.empty())
    {
        int now = que.front();
        que.pop();
        for (int i = 0; i < 26; ++i)
        {
            if (trie[now][i])
            {
                fail[trie[now][i]] = trie[fail[now]][i];
                que.push(trie[now][i]);
            }
            else
            {
                trie[now][i] = trie[fail[now]][i];
            }
        }
    }
}
//打印模式串在主串出现的位置，并返回出现的次数 
int match()
{
    int len = strlen(s), rt = 0, cnt = 0, now;
    for (int i = 0; i < len; ++i)
    {
        now = rt = trie[rt][s[i] - 'a'];
        while (now)
        {
            if (num[now])
            {
                cnt += num[now];
                printf("%d\n", i - slen[now] + 2);
                num[now] = 0;
            }
            now = fail[now];
        }
    }
    return cnt;
}

//下面两个函数打印出值理解用
void p_fail()
{
    for (int i = 0; i < 17; ++i)
        printf("fail[%d] = %d\n", i, fail[i]);
}

void p_trie()
{
    for (int i = 0; i < 13; ++i)
    {
        for (int j = 0; j < 26; ++j)
        {
            if (trie[i][j])
            {
                printf("trie[%d][%d] = %d\n", i, j, trie[i][j]);
            }
        }
    }
}
```
