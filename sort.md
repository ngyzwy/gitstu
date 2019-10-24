## 冒泡排序

``` c++
void bubble_sort(int a[], int l, int r)
{
    int len = r - l + 1;
    for (int i = 1; i < len; ++i)
    {
        for (int j = 0; j < len - i; ++j)
        {
            if (a[j] > a[j + 1])
            {
                swap(a[j], a[j + 1]);
            }
        }
    }
}
```

## 选择排序

```c++
void select_sort(int a[], int l, int r)
{
    int len = r - l + 1;
    for (int i = 0; i < len - 1; ++i)
    {
        int minn = i;
        for (int j = i + 1; j < len; ++j)
        {
            if (a[j] < a[minn])
            {
                minn = j;
            }
        }
        swap(a[i], a[minn]);
    }
}
```

## 快速排序

```c++
void quick_sort(int a[], int l, int r)
{
    if (l >= r)
    {
        return;
    }
    int i = l - 1, j = r + 1, x = a[(l + r) >> 1];
    while (i < j)
    {
        do
        {
            i++;
        } while (a[i] < x);
        do
        {
            j--;
        } while (a[i] > x);
        if (i < j)
        {
            swap(a[i], a[j];
        }
    }
    quick_sort(a, l, j);
    quick_sort(a, j + 1, r);
}
```
