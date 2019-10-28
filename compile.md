## 编译C++文件基本命令

一个C/C++源代码要变成一个可执行文件，需要经过预处理(Pre-processing)－编译(Compiling)－汇编(Assembling)－链接(Link)

基本流程为：源文件`test.c` -> 预处理`test.i` -> 编译`test.s` -> 汇编`test.o` -> 链接`test.out / test.exe`

### 预处理

`-E`选项使用`g++/gcc`将源代码预处理后不执行其他动作。

下面的命令将`test.cpp`预处理，并在标准输出中显示：

`g++ -E test.cpp` 

后面加上`-o`选项表示将源代码预处理后输出在指定文件中，比如`test.i`：

`g++ -E test.cpp -o test.i`

### 编译

`-S`选项使用`g++/gcc`将预处理后的文件编译，翻译成汇编代码。只编译不汇编

下面的命令将会编译`test.i`文件，并自动在当前文件夹生成`test.s`文件

`g++ -S test.i`

若要指定其他输出名，则需`-o`指定，比如生成名为`xxx.s`的汇编代码文件

`g++ -S test.i -o xxx.s`

### 汇编

`-c`选项将编译生成的`test.s`文件生成二进制目标代码

下面的命令将在当前文件夹自动生成`test.o`的二进制目标代码文件

`g++ -c test.s`

如果要指定输出文件名，则需`-o`指定，比如生成`xxx.o`的二进制目标代码文件

`g++ -c test.s -o xxx.o`

### 链接

链接阶段是将相关的目标文件链接起来，形成一个整体，生成可执行文件，是无选项链接

下面的命令会把二进制目标文件`test.o`所需的相关文件链接成一个整体，并在当前文件夹自动生成一个名为`a.out`的可执行文件

`g++ test.o`

如果要执行这个可执行文件，需要输入命令

`./a.out`

当然也可以指定生成的可执行文件的文件名

`g++ test.o -o test.out`

### 单个源文件直接生成可执行文件

当然`g++/gcc`也可以直接把源代码直接生成可执行文件

下面的命令将`test.cpp`直接在当前文件夹生成`a.out`可执行文件，若要指定文件名，可使用`-o`选项

`g++ test.cpp`

`g++ test.cpp -o test.out`

### 多个源文件直接生成可执行文件

也可以将多个源代码编译链接成一个可执行文件

下面的命令将`test1.cpp test2.cpp`直接在当前文件夹生成`a.out`可执行文件，若要指定文件名，可使用 `-o` 选项

`g++ test1.cpp test2.cpp`

`g++ test1.cpp test2.cpp -o test.out`

### 选项`-g`产生调试信息

`g++ test.cpp -o test.out -g`

### 选项`-Wall`输出警告信息

`g++ test.cpp -o test.out -Wall`

### 使用`C++11`标准编译

如果要使用`C++11`版本特性，则需要使用 `-std=c++11` 选项

`g++ -std=c++11 test.cpp -o test.out`
