## 队列清空

``` c++
queue <int> que;
//方法一，用空队列赋值 
que = queue<int>();
//方法二，遍历弹出队列
while (que.size())
    que.pop();
//方法三，用swap(高效)
void clear(queue<int> &q)
{
    queue<int> empty;
    swap(empty, q);
}
```

## 优先队列排序规则及清空

``` c++
priority_queue <int> pq;                            //默认从大到小
priority_queue <int, vector<int>, less<int>> pq;    //less从大到小 
priority_queue <int, vector<int>, greater<int>> pq; //greater从小到大 

//方法一，用空队列赋值 
pq = priority_queue<int>();
//方法二，遍历弹出队列
while (pq.size())
    pq.pop();
//方法三，用swap(高效)
void clear(queue<int> &q)
{
    priority_queue<int> empty;
    swap(empty, q);
}
```
