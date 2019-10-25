## BFS广度优先搜索

> 空间是指数级别的，大！

> 不会有爆栈的风险

> 搜最短，最小

``` c++
void bfs ()
{
    que.push(head);         //起点入队 
    vis[head] = 1;          //标记起点已访问 
    while (que.size())      //队列不为空循环 
    {
        tmp = que.front();  //取出队首元素 
        que.pop();          //队首元素出队 
        if (tmp为目标状体)
            输出或记录
        for (尝试每一种可能)
        {
            if (tmp不合法)
                continue;
            if (tmp合法)
                que.push(tmp + Δ);
         } 
    }
}
```
