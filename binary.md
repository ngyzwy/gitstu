## 二分

```c++
int arr[MAXN];

int binary_search(int l, int y, int key)
{
	int mid;
	while (l <= r)
	{
		mid = l + ((r - l) >> 1); //防止溢出
		if (arr[mid] == key)
		{
			return mid;
		}
		if (arr[mid] < key)
		{
			l = mid + 1;
		}
		else
		{
			r = mid - 1;
		}
	}
	return -1; //没有找到
}
```

## 递归二分

```c++
int arr[MAXN];
int binary_search_recursive(int l, int r, int key)
{
	if (l > r)
	{
		return -1;
	}
	int mid = l + ((r - l) >> 1); //防溢出
	if (arr[mid] == key)
	{
		return mid;
	}
	if (arr[mid] < key)
	{
		return binary_search_recursive(mid + 1, r, key);
	}
	else
	{
		return binary_search_recursive(l, mid - 1, key);
	}
}
```
