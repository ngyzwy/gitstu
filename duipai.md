## 对拍

### 将所有的文件保存在同一目录下，双击启动`duipai.bat`

>找到一份AC的代码保存并编译出`ac.exe`文件

``` c++
#include <iostream>
using namespace std;

int main ()
{
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
```

>你自己的WA的代码保存并编译出`ac.exe`文件

``` c++
#include <iostream>
using namespace std;

int main ()
{
    int a, b;
    cin >> a >> b;
    cout << a - b << endl;
    return 0;
}
```

>编写一个数据生成器并编译为`data.exe`文件

``` c++
#include <iostream>
#include <sstream>
#include <cstdlib>
#include <cstdio>
#include <ctime>

#define random(a, b) (rand()%(b-a+1)+a)

using namespace std;

int main (int argc, char *argv[])
{
    int seed = time(NULL);
    stringstream ss; 
    if (argc > 1) //如果有参数
    {
        ss.clear();
        ss << argv[1];
        ss >> seed; //把参数转换成整数赋值给seed 
    }
    srand(seed);
    //以上生成随机数代码请勿修改
    
    cout << random(1, 10000) << " " << random(1, 10000) << endl;
    
    return 0;
}

/*
用宏定义
产生一定范围随机数的通用表示公式是：
取得(0,x)的随机整数：rand()%x；
取得(a,b)的随机整数：rand()%(b-a)；
取得[a,b)的随机整数：rand()%(b-a)+a；
取得[a,b]的随机整数：rand()%(b-a+1)+a；
取得(a,b]的随机整数：rand()%(b-a)+a+1；
取得0-1之间的浮点数：rand()/double(RAND_MAX)
*/
```

>将下面代码保存为一个`duipai.bat`文件

```
@echo off
:loop
    data.exe %random% > in.txt
    ac.exe < in.txt > ac.txt
    wa.exe < in.txt > wa.txt
    fc ac.txt wa.txt
    pause
if not errorlevel 1 goto loop
goto loop
```
