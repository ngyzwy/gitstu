## 哈希表

``` c++
const int N = 1e3 + 3;
const int M = 99;
int tot = 0; //哈希表节点计数 
int h[M]; //初始化为-1，类似head数组 

struct node {
    int  nxt, info;
}hashNode[N];

void init()
{
    for (int i = 0; i < N; ++i)
        h[i] = -1;
}

void insert(int key, int info)
{
    int u = key % M;
    hashNode[tot] = (node) { h[u], info };
    h[u] = tot++;
}

int find(int key, int info)
{
    int u = key % M;
    for (int i = h[u]; i != -1; i = hashNode[i].nxt)
    {
        if (hashNode[i].info == info)
            return 1;
    }
    return 0;
}
```

## 字符串哈希

[参考博客](https://blog.csdn.net/pengwill97/article/details/80879387)&emsp;

``` c++
const int p = 1e9 + 7;
const int M = 1610612741;
unsigned long long hash[99];
char str[99];
//BKDRHash
int BKDRHash(char *str)
{
    int ans = 0;
    for (int i = 0; str[i]; ++i)
        ans = (ans * p + str[i]) % M;
    return ans;
}
//单哈希方法
int Hash()
{
    hash[0] = 0;
    for (int i = 1; str[i]; ++i)
        hash[i] = (hash[i - 1] * p + str[i]) % M;
    return hash[strlen(str) - 1];
}

/*
双Hash方法,这种Hash很安全 
将一个字符串用不同的mod hash两次，将这两个结果用一个二元组表示，作为Hash结果。
hash1[i] = (hash1[i - 1]) * p + idx(s[i]) % mod1;
hash2[i] = (hash2[i - 1]) * p + idx(s[i]) % mod2;
hash结果为<hash1[n], hash2[n]>

idx(x) = x - 'a' + 1 //也可以用x的ascll值 

求子串的哈希公式
hash = ((hash[r] - hash[l - 1] * p ^ (r - l + 1)) 5 M + M) % M;

预处理p的n的方效果更佳
*/
```

## 拉链法处理hash冲突

```c++
const int SIZE = 1000000;
const int M = 999997;
struct HashTable {
	struct Node {
		int next, value, key;
	} data[SIZE];
	int head[M], size;
	int f(int key) {
		return key % M;
	}
	int get(int key) {
		for (int p = head[f(key)]; p; p = data[p].next)
			if (data[p].key == key) return data[p].value;
		return -1;
	}
	int modify(int key, int value) {
		for (int p = head[f(key)]; p; p = data[p].next)
			if (data[p].key == key) return data[p].value = value;
	}
	int add(int key, int value) {
		if (get(key) != -1) return -1;
		data[++size] = (Node) {
			head[f(key)], value, key
		};
		head[f(key)] = size;
		return value;
	}
};
```

## 封装过的模板，可以像 map 一样用

```c++
struct hash_map {  // 哈希表模板
	struct data {
		long long u;
		int v, nex;
	};                // 前向星结构
	data e[SZ << 1];  // SZ 是 const int 表示大小
	int h[SZ], cnt;
	int hash(long long u) {
		return u % SZ;
	}
	int& operator[](long long u) {
		int hu = hash(u);  // 获取头指针
		for (int i = h[hu]; i; i = e[i].nex)
			if (e[i].u == u) return e[i].v;
		return e[++cnt] = (data) {u, -1, h[hu]}, h[hu] = cnt, e[cnt].v;
	}
	hash_map() {
		cnt = 0;
		memset(h, 0, sizeof(h));
  }
};
```
