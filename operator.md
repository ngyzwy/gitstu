## 运算符重载

``` c++
//结构体中重载
struct Node {
    int x;
    bool operator < (const Node &a) const
    {
        return a.x < x; //从小到大 
    }
};

//结构体外重载
int operator + (Node a, Node b) //必须具有类或灭据类型的参数
{
    return a.x - b.x;
}
```
