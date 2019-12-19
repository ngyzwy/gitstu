## Linux基础知识

Linux系统： “所见皆文件”


Linux系统目录：

	bin：存放二进制可执行文件
	
	boot：存放开机启动程序
	
	dev：存放设备文件： 字符设备、块设备
	
	home：存放普通用户
	
	etc：用户信息和系统配置文件 passwd、group
	
	lib：库文件：libc.so.6
	
	root：管理员宿主目录（家目录）
	
	usr：用户资源管理目录

Linux系统文件类型： 7/8 种

	普通文件：-
	
	目录文件：d
	
	字符设备文件：c
	
	块设备文件：b
	
	软连接：l
	
	管道文件：p
	
	套接字：s
	
	未知文件。

软连接：快捷方式

	为保证软连接可以任意搬移， 创建时务必对源文件使用 绝对路径。

硬链接：

	ln file  file.hard
	
	操作系统给每一个文件赋予唯一的 inode，当有相同inode的文件存在时，彼此同步。
	
	删除时，只将硬链接计数减一。减为0时，inode 被释放。

创建用户：

	sudo adduser 新用户名		--- useradd

修改文件所属用户：

	sudo chown 新用户名 待修改文件。
	
	sudo chown wangwu a.c

删除用户：

	sudo deluser 用户名

创建用户组：

	sudo addgroup 新组名

修改文件所属用户组：

	sudo chgrp 新用户组名 待修改文件。
	
	sudo chgrp g88 a.c

删除组：

	sudo delgroup 用户组名


使用chown 一次修改所有者和所属组：

	sudo chown 所有者：所属组  待操作文件。


find命令：找文件

	-type 按文件类型搜索  d/p/s/c/b/l/ f:文件
	
	-name 按文件名搜索
	
		find ./ -name "*file*.jpg"
	
	-maxdepth 指定搜索深度。应作为第一个参数出现。
	
		find ./ -maxdepth 1 -name "*file*.jpg"


	-size 按文件大小搜索. 单位：k、M、G
	
		find /home/itcast -size +20M -size -50M
	
	-atime、mtime、ctime 天  amin、mmin、cmin 分钟。
	
	-exec：将find搜索的结果集执行某一指定命令。
	
		find /usr/ -name '*tmp*' -exec ls -ld {} \;
	
	-ok: 以交互式的方式 将find搜索的结果集执行某一指定命令


	-xargs：将find搜索的结果集执行某一指定命令。  当结果集数量过大时，可以分片映射。
	
		find /usr/ -name '*tmp*' | xargs ls -ld 
	
	-print0：
		find /usr/ -name '*tmp*' -print0 | xargs  -0 ls -ld 


grep命令：找文件内容

	grep -r 'copy' ./ -n
	
		-n参数：:显示行号
	
	ps aux | grep 'cupsd'  -- 检索进程结果集。


软件安装：

	1. 联网
	
	2. 更新软件资源列表到本地。  sudo apt-get update
	
	3. 安装 sudo apt-get install 软件名
	
	4. 卸载	sudo apt-get remove 软件名
	
	5. 使用软件包（.deb） 安装：	sudo dpkg -i 安装包名。

tar压缩：

	1. tar -zcvf 要生成的压缩包名	压缩材料。
	
		tar zcvf  test.tar.gz  file1 dir2   使用 gzip方式压缩。
	
		tar jcvf  test.tar.gz  file1 dir2   使用 bzip2方式压缩。

tar解压：

	将 压缩命令中的 c --> x
	
		tar zxvf  test.tar.gz   使用 gzip方式解压缩。
	
		tar jxvf  test.tar.gz   使用 bzip2方式解压缩。

rar压缩：

	rar a -r  压缩包名（带.rar后缀） 压缩材料。
	
		rar a -r testrar.rar	stdio.h test2.mp3

rar解压：

	unrar x 压缩包名（带.rar后缀）

zip压缩：

	zip -r 压缩包名（带.zip后缀） 压缩材料。
	
		zip -r testzip.zip dir stdio.h test2.mp3

zip解压：

	unzip 压缩包名（带.zip后缀） 
	
		unzip  testzip.zip 
![Unix家谱](Unix家谱.jpg)

![Unix系统体系结构](Unix系统体系结构.png)

![磁盘](磁盘.png)

![服务器](服务器.png)

![安装服务器](安装服务器.png)

## vim基本操作

跳转到指定行：

	1. 88G （命令模式）
	
	2. :88  (末行模式)

跳转文件首：

	gg （命令模式）

跳转文件尾：

	G（命令模式）

自动格式化程序：

	gg=G（命令模式）set shiftwidth=4

大括号对应：

	% （命令模式）

光标移至行首：

	0 （命令模式）执行结束，工作模式不变。

光标移至行尾：

	$ （命令模式）执行结束，工作模式不变。

删除单个字符：

	x （命令模式）执行结束，工作模式不变。

替换单个字符：

	将待替换的字符用光标选中， r （命令模式），再按欲替换的字符

删除一个单词：

	dw（命令模式）光标置于单词的首字母进行操作。

删除光标至行尾：

	D 或者 d$（命令模式）

删除光标至行首：

	d0 （命令模式）

删除指定区域：

	按 V （命令模式）切换为 “可视模式”，使用 hjkl挪移光标来选中待删除区域。  按 d 删除该区域数据。

删除指定1行：

	在光标所在行，按 dd （命令模式）


删除指定N行：

	在光标所待删除首行，按 Ndd （命令模式）

复制一行：

	yy

粘贴：

```
p：向后、P：向前。
```

查找：

	1. 找 设想 内容：
		命令模式下， 按 “/” 输入欲搜索关键字，回车。使用 n 检索下一个。
	
	2. 找 看到的内容：
	
		命令模式下，将光标置于单词任意一个字符上，按 “*”/ “#” 

单行替换：

	将光标置于待替换行上， 进入末行模式，输入 :s /原数据/新数据

通篇替换：

	末行模式， :%s /原数据/新数据/g   g:不加，只替换每行首个。   sed 

指定行的替换：

	末行模式， :起始行号，终止行号s /原数据/新数据/g   g:不加，只替换每行首个。
	
		:29,35s /printf/println/g

撤销、反撤销：

	u、ctrl+r（命令模式）

分屏：

	sp：横屏分。 Ctrl+ww 切换。
	vsp：竖屏分。Ctrl+ww 切换。

跳转至 man 手册：

	将光标置于待查看函数单词上，使用 K（命令模式）跳转。 指定卷， nK

查看宏定义：

	将光标置于待查看宏定义单词上，使用 [d 查看定义语句。


在末行模式执行shell命令：

	:!命令		:! ls -l 

## 动态库静态库

gcc编译：

	4步骤： 预处理、编译、汇编、连接。
	
	-I：	指定头文件所在目录位置。
	
	-c：	只做预处理、编译、汇编。得到 二进制 文件！！！
	
	-g：	编译时添加调试语句。 主要支持 gdb 调试。
	
	-Wall： 显示所有警告信息。
	
	-D：	向程序中“动态”注册宏定义。   #define NAME VALUE


静态库制作及使用步骤：

	1. 将 .c 生成 .o 文件
	
		gcc -c add.c -o add.o
	
	2. 使用 ar 工具制作静态库
	
		ar rcs  lib库名.a  add.o sub.o div.o
	
	3. 编译静态库到可执行文件中：
	
		gcc test.c lib库名.a -o a.out


头文件守卫：防止头文件被重复包含

	#ifndef _HEAD_H_
	
	#define _HEAD_H_
	
	......
	
	#endif


动态库制作及使用：

	1.  将 .c 生成 .o 文件， （生成与位置无关的代码 -fPIC）
	
		gcc -c add.c -o add.o -fPIC
	
	2. 使用 gcc -shared 制作动态库
	
		gcc -shared -o lib库名.so	add.o sub.o div.o
	
	3. 编译可执行程序时，指定所使用的动态库。  -l：指定库名(去掉lib前缀和.so后缀)  -L：指定库路径。
	
		gcc test.c -o a.out -lmymath -L./lib
	
	4. 运行可以执行程序 ./a.out 出错！！！！ --- ldd a.out --> "not found"
	
		error while loading shared libraries: libxxx.so: cannot open shared object file: No such file or directory
	
		原因：
			链接器：	工作于链接阶段， 工作时需要 -l 和 -L
	
			动态链接器：	工作于程序运行阶段，工作时需要提供动态库所在目录位置。
	
		解决方式：				
	
			【1】 通过环境变量：  export LD_LIBRARY_PATH=动态库路径
	
				./a.out 成功！！！  （临时生效， 终端重启环境变量失效）
	
			【2】 永久生效： 写入 终端配置文件。  .bashrc  建议使用绝对路径。
	
				1) vi ~/.bashrc
	
				2) 写入 export LD_LIBRARY_PATH=动态库路径  保存
	
				3）. .bashrc/  source .bashrc / 重启 终端  ---> 让修改后的.bashrc生效
	
				4）./a.out 成功！！！ 
	
			【3】 拷贝自定义动态库 到 /lib (标准C库所在目录位置)
	
			【4】 配置文件法
	
				1）sudo vi /etc/ld.so.conf
	
				2) 写入 动态库绝对路径  保存
	
				3）sudo ldconfig -v  使配置文件生效。
	
				4）./a.out 成功！！！--- 使用 ldd  a.out 查看
![工作模式](工作模式.png)

![数据段合并](数据段合并.png)

![gcc编译4步骤](gcc编译4步骤.png)

![动态库和静态库](动态库和静态库.png)

## GDB调试与Makefile编译

gdb调试工具：   大前提：程序是你自己写的。  ---逻辑错误


基础指令：

	-g：使用该参数编译可以执行文件，得到调试表。
	
	gdb ./a.out
	
	list： list 1  列出源码。根据源码指定 行号设置断点。
	
	b：	b 20	在20行位置设置断点。
	
	run/r:	运行程序
	
	n/next: 下一条指令（会越过函数）
	
	s/step: 下一条指令（会进入函数）
	
	p/print：p i  查看变量的值。
	
	continue：继续执行断点后续指令。
	
	finish：结束当前函数调用。 
	
	quit：退出gdb当前调试。

其他指令：

	run：使用run查找段错误出现位置。
	
	set args： 设置main函数命令行参数 （在 start、run 之前）
	
	run 字串1 字串2 ...: 设置main函数命令行参数
	
	info b: 查看断点信息表
	
	b 20 if i = 5：	设置条件断点。
	
	ptype：查看变量类型。
	
	bt：列出当前程序正存活着的栈帧。
	
	frame： 根据栈帧编号，切换栈帧。
	
	display：设置跟踪变量
	
	undisplay：取消设置跟踪变量。 使用跟踪变量的编号。


makefile： 管理项目。

	命名：makefile	 Makefile  --- make 命令
	
	1 个规则：
	
		目标：依赖条件
		（一个tab缩进）命令
	
		1. 目标的时间必须晚于依赖条件的时间，否则，更新目标
	
		2. 依赖条件如果不存在，找寻新的规则去产生依赖条件。
	
	ALL：指定 makefile 的终极目标。
	
	2 个函数：
	
		src = $(wildcard ./*.c): 匹配当前工作目录下的所有.c 文件。将文件名组成列表，赋值给变量 src。  src = add.c sub.c div1.c 
	
		obj = $(patsubst %.c, %.o, $(src)): 将参数3中，包含参数1的部分，替换为参数2。 obj = add.o sub.o div1.o
	
	clean:	(没有依赖)
	
		-rm -rf $(obj) a.out	“-”：作用是，删除不存在文件时，不报错。顺序执行结束。
	
	3 个自动变量：
	
		$@: 在规则的命令中，表示规则中的目标。
	
		$^: 在规则的命令中，表示所有依赖条件。
	
		$<: 在规则的命令中，表示第一个依赖条件。如果将该变量应用在模式规则中，它可将依赖条件列表中的依赖依次取出，套用模式规则。
	
	模式规则：
	
		%.o:%.c
		   gcc -c $< -o %@
	
	静态模式规则：
	
		$(obj):%.o:%.c
		   gcc -c $< -o %@	
	
	伪目标：
	
		.PHONY: clean ALL
	
	参数：
		-n：模拟执行make、make clean 命令。
	
		-f：指定文件执行 make 命令。				xxxx.mk

## 文件IO

open函数：

	int open(char *pathname, int flags)	#include <unistd.h>
	
	参数：
		pathname: 欲打开的文件路径名
	
		flags：文件打开方式：	#include <fcntl.h>
	
			O_RDONLY|O_WRONLY|O_RDWR	O_CREAT|O_APPEND|O_TRUNC|O_EXCL|O_NONBLOCK ....
	
	返回值：
		成功： 打开文件所得到对应的 文件描述符（整数）
	
		失败： -1， 设置errno	
	
	int open(char *pathname, int flags， mode_t mode)		123  775	
	
	参数：
		pathname: 欲打开的文件路径名
	
		flags：文件打开方式：	O_RDONLY|O_WRONLY|O_RDWR	O_CREAT|O_APPEND|O_TRUNC|O_EXCL|O_NONBLOCK ....
	
		mode: 参数3使用的前提， 参2指定了 O_CREAT。	取值8进制数，用来描述文件的 访问权限。 rwx    0664
	
			创建文件最终权限 = mode & ~umask
	
	返回值：
		成功： 打开文件所得到对应的 文件描述符（整数）
	
		失败： -1， 设置errno	

close函数：

	int close(int fd);


错误处理函数：		与 errno 相关。

	printf("xxx error: %d\n", errno);
	
	char *strerror(int errnum);
	
		printf("xxx error: %s\n", strerror(errno));
	
	void perror(const char *s);
	
		perror("open error");


read函数：

	ssize_t read(int fd, void *buf, size_t count);
	
	参数：
		fd：文件描述符
	
		buf：存数据的缓冲区
	
		count：缓冲区大小
	
	返回值：
	
		0：读到文件末尾。
	
		成功；	> 0 读到的字节数。
	
		失败：	-1， 设置 errno
	
		-1： 并且 errno = EAGIN 或 EWOULDBLOCK, 说明不是read失败，而是read在以非阻塞方式读一个设备文件（网络文件），并且文件无数据。

write函数：

	ssize_t write(int fd, const void *buf, size_t count);
	
	参数：
		fd：文件描述符
	
		buf：待写出数据的缓冲区
	
		count：数据大小
	
	返回值：
	
		成功；	写入的字节数。
	
		失败：	-1， 设置 errno

文件描述符：

	PCB进程控制块：本质 结构体。
	
	成员：文件描述符表。
	
	文件描述符：0/1/2/3/4。。。。/1023     表中可用的最小的。
	
	0 - STDIN_FILENO
	
	1 - STDOUT_FILENO
	
	2 - STDERR_FILENO

阻塞、非阻塞：  是设备文件、网络文件的属性。

	产生阻塞的场景。 读设备文件。读网络文件。（读常规文件无阻塞概念。）
	
	/dev/tty -- 终端文件。
	
	open("/dev/tty", O_RDWR|O_NONBLOCK)	--- 设置 /dev/tty 非阻塞状态。(默认为阻塞状态)

fcntl：

	int (int fd, int cmd, ...)
	
	int flgs = fcntl(fd,  F_GETFL);
	
	flgs |= O_NONBLOCK
	
	fcntl(fd,  F_SETFL, flgs);
	
	获取文件状态： F_GETFL
	
	设置文件状态： F_SETFL

lseek函数：

	off_t lseek(int fd, off_t offset, int whence);
	
	参数：
		fd：文件描述符
	
		offset： 偏移量
	
		whence：起始偏移位置： SEEK_SET/SEEK_CUR/SEEK_END
	
	返回值：
	
		成功：较起始位置偏移量
	
		失败：-1 errno
	
	应用场景：	
		1. 文件的“读”、“写”使用同一偏移位置。
	
		2. 使用lseek获取文件大小
	
		3. 使用lseek拓展文件大小：要想使文件大小真正拓展，必须引起IO操作。
	
			使用 truncate 函数，直接拓展文件。	int ret = truncate("dict.cp", 250);

传入参数：

	1. 指针作为函数参数。
	
	2. 同常有const关键字修饰。
	
	3. 指针指向有效区域， 在函数内部做读操作。

传出参数：

	1. 指针作为函数参数。
	
	2. 在函数调用之前，指针指向的空间可以无意义，但必须有效。
	
	3. 在函数内部，做写操作。
	
	4。函数调用结束后，充当函数返回值。

传入传出参数：

	1. 指针作为函数参数。
	
	2. 在函数调用之前，指针指向的空间有实际意义。
	
	3. 在函数内部，先做读操作，后做写操作。
	
	4. 函数调用结束后，充当函数返回值。
	
	 void aaa();
	
	 int aaa(int *p, struct stat *p2, strcut student *p3);
	
	 bbb()
	 {
		aaa();
	 }

stat/lstat 函数：

	int stat(const char *path, struct stat *buf);
	
	参数：
		path： 文件路径
	
		buf：（传出参数） 存放文件属性。
	
	返回值：
	
		成功： 0
	
		失败： -1 errno
	
	获取文件大小： buf.st_size
	
	获取文件类型： buf.st_mode
	
	获取文件权限： buf.st_mode
	
	符号穿透：stat会。lstat不会。

link/unlink:

	隐式回收。


目录操作函数：

	DIR * opendir(char *name);
	
	int closedir(DIR *dp);
	
	struct dirent *readdir(DIR * dp);
	
		struct dirent {
	
			inode
	
			char dname[256];
		}
![fcntl设置文件属性](fcntl设置文件属性.png)

![库函数和系统调用](库函数和系统调用.png)

![目录项和inode](目录项和inode.png)

![文件权限位图](文件权限位图.png)

![预读入缓输出机制](预读入缓输出机制.png)

[file_IO](file_IO_test.zip)

[fileSystem](fileSystem_test.zip)



递归遍历目录：ls-R.c

	1. 判断命令行参数，获取用户要查询的目录名。	int argc, char *argv[1]
	
		argc == 1  --> ./
	
	2. 判断用户指定的是否是目录。 stat  S_ISDIR(); --> 封装函数 isFile() {   }
	
	3. 读目录： read_dir() { 
	
		opendir（dir）
	
		while （readdir（））{
	
			普通文件，直接打印
	
			目录：
				拼接目录访问绝对路径。sprintf(path, "%s/%s", dir, d_name) 
	
				递归调用自己。--》 opendir（path） readdir closedir
		}
	
		closedir（）
	
		}
		read_dir() --> isFile() ---> read_dir()

dup 和 dup2：

	int dup(int oldfd);		文件描述符复制。
	
		oldfd: 已有文件描述符
	
		返回：新文件描述符。
	
	int dup2(int oldfd, int newfd); 文件描述符复制。重定向。

fcntl 函数实现 dup：

	int fcntl(int fd, int cmd, ....)
	
	cmd: F_DUPFD
	
	参3:  	被占用的，返回最小可用的。
	
		未被占用的， 返回=该值的文件描述符。

进程：

	程序：死的。只占用磁盘空间。		——剧本.
	
	进程；活的。运行起来的程序。占用内存、cpu等系统资源。	——戏。

PCB进程控制块：

	进程id
	
	文件描述符表
	
	进程状态：	初始态、就绪态、运行态、挂起态、终止态。
	
	进程工作目录位置
	
	*umask掩码 
	
	信号相关信息资源。
	
	用户id和组id

fork函数：

	pid_t fork(void)
	
	创建子进程。父子进程各自返回。父进程返回子进程pid。 子进程返回 0.
	
	getpid();getppid();
	
	循环创建N个子进程模型。 每个子进程标识自己的身份。

父子进程相同：

	刚fork后。 data段、text段、堆、栈、环境变量、全局变量、宿主目录位置、进程工作目录位置、信号处理方式


父子进程不同：

	进程id、返回值、各自的父进程、进程创建时间、闹钟、未决信号集

父子进程共享：

	读时共享、写时复制。———————— 全局变量。
	
	1. 文件描述符 2. mmap映射区。
![fork函数](fork函数.png)

![物理内存和虚拟内存](物理内存和虚拟内存.png)

![fork N个子进程](fork N个子进程.png)

[ls-Rdir_dup_test](ls-Rdir_dup_test)

[process_test](process_test)

## 进程通信

gdb调试：

	设置父进程调试路径：set follow-fork-mode parent (默认)
	
	设置子进程调试路径：set follow-fork-mode child


exec函数族：

	使进程执行某一程序。成功无返回值，失败返回 -1
	
	int execlp(const char *file, const char *arg, ...);		借助 PATH 环境变量找寻待执行程序
	
		参1： 程序名
	
		参2： argv0
	
		参3： argv1
	
		...： argvN
	
		哨兵：NULL
	
	int execl(const char *path, const char *arg, ...);		自己指定待执行程序路径。
	
	int execvp();

ps ajx --> pid ppid gid sid 


孤儿进程：

	父进程先于子进终止，子进程沦为“孤儿进程”，会被 init 进程领养。

僵尸进程：

	子进程终止，父进程尚未对子进程进行回收，在此期间，子进程为“僵尸进程”。  kill 对其无效。


wait函数：	回收子进程退出资源， 阻塞回收任意一个。

	pid_t wait(int *status)
	
	参数：（传出） 回收进程的状态。
	
	返回值：成功： 回收进程的pid
	
		失败： -1， errno
	
	函数作用1：	阻塞等待子进程退出
	
	函数作用2：	清理子进程残留在内核的 pcb 资源
	
	函数作用3：	通过传出参数，得到子进程结束状态


​	
​	获取子进程正常终止值：
​	
		WIFEXITED(status) --》 为真 --》调用 WEXITSTATUS(status) --》 得到 子进程 退出值。
	
	获取导致子进程异常终止信号：
	
		WIFSIGNALED(status) --》 为真 --》调用 WTERMSIG(status) --》 得到 导致子进程异常终止的信号编号。


waitpid函数：	指定某一个进程进行回收。可以设置非阻塞。			waitpid(-1, &status, 0) == wait(&status);

	pid_t waitpid(pid_t pid, int *status, int options)
	
	参数：
		pid：指定回收某一个子进程pid
	
			> 0: 待回收的子进程pid
	
			-1：任意子进程
	
			0：同组的子进程。
	
		status：（传出） 回收进程的状态。
	
		options：WNOHANG 指定回收方式为，非阻塞。
	
	返回值：
	
		> 0 : 表成功回收的子进程 pid
	
		0 : 函数调用时， 参3 指定了WNOHANG， 并且，没有子进程结束。
	
		-1: 失败。errno


总结：

	wait、waitpid	一次调用，回收一个子进程。
	
			想回收多个。while 

===========================

进程间通信的常用方式，特征：

	管道：简单
	
	信号：开销小
	
	mmap映射：非血缘关系进程间
	
	socket（本地套接字）：稳定

管道：

	实现原理： 内核借助环形队列机制，使用内核缓冲区实现。
	
	特质；	1. 伪文件
	
		2. 管道中的数据只能一次读取。
	
		3. 数据在管道中，只能单向流动。
	
	局限性：1. 自己写，不能自己读。
	
		2. 数据不可以反复读。
	
		3. 半双工通信。
	
		4. 血缘关系进程间可用。


pipe函数：	创建，并打开管道。

	int pipe(int fd[2]);
	
	参数：	fd[0]: 读端。
	
		fd[1]: 写端。
	
	返回值： 成功： 0
	
		 失败： -1 errno

管道的读写行为：

	读管道：
		1. 管道有数据，read返回实际读到的字节数。
	
		2. 管道无数据：	1）无写端，read返回0 （类似读到文件尾）
	
				2）有写端，read阻塞等待。
	
	写管道：
		1. 无读端， 异常终止。 （SIGPIPE导致的）
	
		2. 有读端：	1） 管道已满， 阻塞等待
	
				2） 管道未满， 返回写出的字节个数。
![exec函数](exec函数.png)

![管道通信](管道通信.png)

![管道原理图](管道原理图.png)

[pipe](pipe)

[process](process)

[wait课堂演示代码](wait课堂演示代码)

pipe管道： 用于有血缘关系的进程间通信。  ps aux | grep 		ls | wc -l	

	父子进程间通信：


	兄弟进程间通信：



fifo管道：可以用于无血缘关系的进程间通信。

	命名管道：  mkfifo 
	
	无血缘关系进程间通信：
	
		读端，open fifo O_RDONLY
	
		写端，open fifo O_WRONLY


文件实现进程间通信：

	打开的文件是内核中的一块缓冲区。多个无血缘关系的进程，可以同时访问该文件。


共享内存映射:

void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);		创建共享内存映射

	参数：
		addr： 	指定映射区的首地址。通常传NULL，表示让系统自动分配
	
		length：共享内存映射区的大小。（<= 文件的实际大小）
	
		prot：	共享内存映射区的读写属性。PROT_READ、PROT_WRITE、PROT_READ|PROT_WRITE
	
		flags：	标注共享内存的共享属性。MAP_SHARED、MAP_PRIVATE
	
		fd:	用于创建共享内存映射区的那个文件的 文件描述符。
	
		offset：默认0，表示映射文件全部。偏移位置。需是 4k 的整数倍。
	
	返回值：
	
		成功：映射区的首地址。
	
		失败：MAP_FAILED (void*(-1))， errno


int munmap(void *addr, size_t length);		释放映射区。

	addr：mmap 的返回值
	
	length：大小


使用注意事项：

	1. 用于创建映射区的文件大小为 0，实际指定非0大小创建映射区，出 “总线错误”。
	
	2. 用于创建映射区的文件大小为 0，实际制定0大小创建映射区， 出 “无效参数”。
	
	3. 用于创建映射区的文件读写属性为，只读。映射区属性为 读、写。 出 “无效参数”。
	
	4. 创建映射区，需要read权限。当访问权限指定为 “共享”MAP_SHARED是， mmap的读写权限，应该 <=文件的open权限。	只写不行。
	
	5. 文件描述符fd，在mmap创建映射区完成即可关闭。后续访问文件，用 地址访问。
	
	6. offset 必须是 4096的整数倍。（MMU 映射的最小单位 4k ）
	
	7. 对申请的映射区内存，不能越界访问。 
	
	8. munmap用于释放的 地址，必须是mmap申请返回的地址。
	
	9. 映射区访问权限为 “私有”MAP_PRIVATE, 对内存所做的所有修改，只在内存有效，不会反应到物理磁盘上。
	
	10.  映射区访问权限为 “私有”MAP_PRIVATE, 只需要open文件时，有读权限，用于创建映射区即可。


mmap函数的保险调用方式：

	1. fd = open（"文件名"， O_RDWR）;
	
	2. mmap(NULL, 有效文件大小， PROT_READ|PROT_WRITE, MAP_SHARED, fd, 0);


父子进程使用 mmap 进程间通信：

	父进程 先 创建映射区。 open（ O_RDWR） mmap( MAP_SHARED );
	
	指定 MAP_SHARED 权限
	
	fork() 创建子进程。
	
	一个进程读， 另外一个进程写。

无血缘关系进程间 mmap 通信：  				【会写】

	两个进程 打开同一个文件，创建映射区。
	
	指定flags 为 MAP_SHARED。
	
	一个进程写入，另外一个进程读出。
	
	【注意】：无血缘关系进程间通信。mmap：数据可以重复读取。
	
					fifo：数据只能一次读取。

匿名映射：只能用于 血缘关系进程间通信。

	p = (int *)mmap(NULL, 40, PROT_READ|PROT_WRITE, MAP_SHARED|MAP_ANONYMOUS, -1, 0);

[UNIX环境高级编程（中文版+英文版+源代码）](UNIX环境高级编程（中文版+英文版+源代码）)

![fifo](fifo.png)

![无血缘关系进程间文件通信](无血缘关系进程间文件通信.png)

![兄弟进程间通信](兄弟进程间通信.png)

[IPC_test](IPC_test)

信号共性：

	简单、不能携带大量信息、满足条件才发送。

信号的特质：

	信号是软件层面上的“中断”。一旦信号产生，无论程序执行到什么位置，必须立即停止运行，处理信号，处理结束，再继续执行后续指令。
	
	所有信号的产生及处理全部都是由【内核】完成的。

信号相关的概念：

	产生信号：
	
		1. 按键产生
	
		2. 系统调用产生
	
		3. 软件条件产生
	
		4. 硬件异常产生
	
		5. 命令产生
	
	概念：
		未决：产生与递达之间状态。  
	
		递达：产生并且送达到进程。直接被内核处理掉。
	
		信号处理方式： 执行默认处理动作、忽略、捕捉（自定义）


		阻塞信号集（信号屏蔽字）： 本质：位图。用来记录信号的屏蔽状态。一旦被屏蔽的信号，在解除屏蔽前，一直处于未决态。
	
		未决信号集：本质：位图。用来记录信号的处理状态。该信号集中的信号，表示，已经产生，但尚未被处理。

信号4要素：

	信号使用之前，应先确定其4要素，而后再用！！！
	
	编号、名称、对应事件、默认处理动作。

kill命令 和 kill函数：

	int kill（pid_t pid, int signum）
	
	参数：
		pid: 	> 0:发送信号给指定进程
	
			= 0：发送信号给跟调用kill函数的那个进程处于同一进程组的进程。
	
			< -1: 取绝对值，发送信号给该绝对值所对应的进程组的所有组员。
	
			= -1：发送信号给，有权限发送的所有进程。
	
		signum：待发送的信号
	
	返回值：
		成功： 0
	
		失败： -1 errno


alarm 函数：使用自然计时法。

	定时发送SIGALRM给当前进程。
	
	unsigned int alarm(unsigned int seconds);
	
		seconds：定时秒数
	
		返回值：上次定时剩余时间。
	
			无错误现象。
	
		alarm（0）； 取消闹钟。
	
	time 命令 ： 查看程序执行时间。   实际时间 = 用户时间 + 内核时间 + 等待时间。  --》 优化瓶颈 IO


setitimer函数：

	int setitimer(int which, const struct itimerval *new_value, struct itimerval *old_value);
	
	参数：
		which：	ITIMER_REAL： 采用自然计时。 ——> SIGALRM
	
			ITIMER_VIRTUAL: 采用用户空间计时  ---> SIGVTALRM
	
			ITIMER_PROF: 采用内核+用户空间计时 ---> SIGPROF
		
		new_value：定时秒数
	
		           类型：struct itimerval {
	
	           				struct timeval {
	           					time_t      tv_sec;         /* seconds */
	           					suseconds_t tv_usec;        /* microseconds */
	
	       				}it_interval;---> 周期定时秒数
	
	           				 struct timeval {
	           					time_t      tv_sec;         
	           					suseconds_t tv_usec;        
	
	       				}it_value;  ---> 第一次定时秒数  
	       			 };
	
		old_value：传出参数，上次定时剩余时间。
	
		e.g.
			struct itimerval new_t;	
			struct itimerval old_t;	
	
			new_t.it_interval.tv_sec = 0;
			new_t.it_interval.tv_usec = 0;
			new_t.it_value.tv_sec = 1;
			new_t.it_value.tv_usec = 0;
	
			int ret = setitimer(&new_t, &old_t);  定时1秒
	
	返回值：
		成功： 0
	
		失败： -1 errno


其他几个发信号函数：

	int raise(int sig);
	
	void abort(void);


信号集操作函数：

	sigset_t set;  自定义信号集。
	
	sigemptyset(sigset_t *set);	清空信号集
	
	sigfillset(sigset_t *set);	全部置1
	
	sigaddset(sigset_t *set, int signum);	将一个信号添加到集合中
	
	sigdelset(sigset_t *set, int signum);	将一个信号从集合中移除
	
	sigismember（const sigset_t *set，int signum); 判断一个信号是否在集合中。 在--》1， 不在--》0

设置信号屏蔽字和解除屏蔽：

	int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);
	
		how:	SIG_BLOCK:	设置阻塞
	
			SIG_UNBLOCK:	取消阻塞
	
			SIG_SETMASK:	用自定义set替换mask。
	
		set：	自定义set
	
		oldset：旧有的 mask。

查看未决信号集：

	int sigpending(sigset_t *set);
	
		set： 传出的 未决信号集。

【信号捕捉】：

	signal();
	
	【sigaction();】 重点！！！


​		

信号捕捉特性：

	1. 捕捉函数执行期间，信号屏蔽字 由 mask --> sa_mask , 捕捉函数执行结束。 恢复回mask
	
	2. 捕捉函数执行期间，本信号自动被屏蔽(sa_flgs = 0).
	
	3. 捕捉函数执行期间，被屏蔽信号多次发送，解除屏蔽后只处理一次！


借助信号完成 子进程回收。

![信号集操作](信号集操作.png)

![阻塞信号集和未决信号集](阻塞信号集和未决信号集.png)

[signal_1](signal_1)

守护进程：

	daemon进程。通常运行与操作系统后台，脱离控制终端。一般不与用户直接交互。周期性的等待某个事件发生或周期性执行某一动作。
	
	不受用户登录注销影响。通常采用以d结尾的命名方式。


守护进程创建步骤：

	1. fork子进程，让父进程终止。
	
	2. 子进程调用 setsid() 创建新会话
	
	3. 通常根据需要，改变工作目录位置 chdir()， 防止目录被卸载。
	
	4. 通常根据需要，重设umask文件权限掩码，影响新文件的创建权限。  022 -- 755	0345 --- 432   r---wx-w-   422
	
	5. 通常根据需要，关闭/重定向 文件描述符
	
	6. 守护进程 业务逻辑。while（）

=============================================================

线程概念：

	进程：有独立的 进程地址空间。有独立的pcb。	分配资源的最小单位。
	
	线程：有独立的pcb。没有独立的进程地址空间。	最小单位的执行。
	
	ps -Lf 进程id 	---> 线程号。LWP  --》cpu 执行的最小单位。

线程共享：

	独享 栈空间（内核栈、用户栈）
	
	共享 ./text./data ./rodataa ./bsss heap  ---> 共享【全局变量】（errno）

线程控制原语：

	pthread_t pthread_self(void);	获取线程id。 线程id是在进程地址空间内部，用来标识线程身份的id号。
	
		返回值：本线程id


	检查出错返回：  线程中。
	
		fprintf(stderr, "xxx error: %s\n", strerror(ret));


	int pthread_create(pthread_t *tid, const pthread_attr_t *attr, void *(*start_rountn)(void *), void *arg); 创建子线程。
	
		参1：传出参数，表新创建的子线程 id
	
		参2：线程属性。传NULL表使用默认属性。
	
		参3：子线程回调函数。创建成功，ptherad_create函数返回时，该函数会被自动调用。
		
		参4：参3的参数。没有的话，传NULL
	
		返回值：成功：0
	
			失败：errno


	循环创建N个子线程：
	
		for （i = 0； i < 5; i++）
	
			pthread_create(&tid, NULL, tfn, (void *)i);   // 将 int 类型 i， 强转成 void *， 传参。	


	void pthread_exit(void *retval);  退出当前线程。
	
		retval：退出值。 无退出值时，NULL
	
		exit();	退出当前进程。
	
		return: 返回到调用者那里去。
	
		pthread_exit(): 退出当前线程。


	int pthread_join(pthread_t thread, void **retval);	阻塞 回收线程。
	
		thread: 待回收的线程id
	
		retval：传出参数。 回收的那个线程的退出值。
	
			线程异常借助，值为 -1。
	
		返回值：成功：0
	
			失败：errno
	
	int pthread_detach(pthread_t thread);		设置线程分离
	
		thread: 待分离的线程id


​	
​		返回值：成功：0
​	
			失败：errno	
	
	int pthread_cancel(pthread_t thread);		杀死一个线程。  需要到达取消点（保存点）
	
		thread: 待杀死的线程id
		
		返回值：成功：0
	
			失败：errno
	
		如果，子线程没有到达取消点， 那么 pthread_cancel 无效。
	
		我们可以在程序中，手动添加一个取消点。使用 pthread_testcancel();
	
		成功被 pthread_cancel() 杀死的线程，返回 -1.使用pthead_join 回收。


	线程控制原语					进程控制原语


	pthread_create()				fork();
	
	pthread_self()					getpid();
	
	pthread_exit()					exit(); 		/ return 
	
	pthread_join()					wait()/waitpid()
	
	pthread_cancel()				kill()
	
	pthread_detach()


线程属性：

	设置分离属性。
	
	pthread_attr_t attr  	创建一个线程属性结构体变量
	
	pthread_attr_init(&attr);	初始化线程属性
	
	pthread_attr_setdetachstate(&attr,  PTHREAD_CREATE_DETACHED);		设置线程属性为 分离态
	
	pthread_create(&tid, &attr, tfn, NULL); 借助修改后的 设置线程属性 创建为分离态的新线程
	
	pthread_attr_destroy(&attr);	销毁线程属性
![进程和线程](进程和线程.png)

![三级映射](三级映射.png)

![最小执行单位](最小执行单位.png)

[pthread_test](pthread_test)

[session_daemon_test](session_daemon_test)

线程同步：

	协同步调，对公共区域数据按序访问。防止数据混乱，产生与时间有关的错误。

锁的使用：

	建议锁！对公共数据进行保护。所有线程【应该】在访问公共数据前先拿锁再访问。但，锁本身不具备强制性。


使用mutex(互斥量、互斥锁)一般步骤：

	pthread_mutex_t 类型。 
	
	1. pthread_mutex_t lock;  创建锁
	
	2  pthread_mutex_init; 初始化		1
	
	3. pthread_mutex_lock;加锁		1--	--> 0
	
	4. 访问共享数据（stdout)		
	
	5. pthrad_mutext_unlock();解锁		0++	--> 1
	
	6. pthead_mutex_destroy；销毁锁


	初始化互斥量：
	
		pthread_mutex_t mutex;
	
		1. pthread_mutex_init(&mutex, NULL);   			动态初始化。
	
		2. pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;	静态初始化。
	
	注意事项：
	
		尽量保证锁的粒度， 越小越好。（访问共享数据前，加锁。访问结束【立即】解锁。）
	
		互斥锁，本质是结构体。 我们可以看成整数。 初值为 1。（pthread_mutex_init() 函数调用成功。）
	
		加锁： --操作， 阻塞线程。
	
		解锁： ++操作， 换醒阻塞在锁上的线程。
	
		try锁：尝试加锁，成功--。失败，返回。同时设置错误号 EBUSY

restrict关键字：

	用来限定指针变量。被该关键字限定的指针变量所指向的内存操作，必须由本指针完成。

【死锁】：

	是使用锁不恰当导致的现象：
	
		1. 对一个锁反复lock。
	
		2. 两个线程，各自持有一把锁，请求另一把。


读写锁：

	锁只有一把。以读方式给数据加锁——读锁。以写方式给数据加锁——写锁。
	
	读共享，写独占。
	
	写锁优先级高。
	
	相较于互斥量而言，当读线程多的时候，提高访问效率
	
	pthread_rwlock_t  rwlock;
	
	pthread_rwlock_init(&rwlock, NULL);
	
	pthread_rwlock_rdlock(&rwlock);		try
	
	pthread_rwlock_wrlock(&rwlock);		try
	
	pthread_rwlock_unlock(&rwlock);
	
	pthread_rwlock_destroy(&rwlock);

条件变量：

	本身不是锁！  但是通常结合锁来使用。 mutex
	
	pthread_cond_t cond;
	
	初始化条件变量：
	
		1. pthread_cond_init(&cond, NULL);   			动态初始化。
	
		2. pthread_cond_t cond = PTHREAD_COND_INITIALIZER;	静态初始化。
	
	阻塞等待条件：
	
		pthread_cond_wait(&cond, &mutex);
	
		作用：	1） 阻塞等待条件变量满足
	
			2） 解锁已经加锁成功的信号量 （相当于 pthread_mutex_unlock(&mutex)）
	
			3)  当条件满足，函数返回时，重新加锁信号量 （相当于， pthread_mutex_lock(&mutex);）


	pthread_cond_signal(): 唤醒阻塞在条件变量上的 (至少)一个线程。
	
	pthread_cond_broadcast()： 唤醒阻塞在条件变量上的 所有线程。


	【要求，能够借助条件变量，完成生成者消费者】

信号量： 

	应用于线程、进程间同步。
	
	相当于 初始化值为 N 的互斥量。  N值，表示可以同时访问共享数据区的线程数。
	
	函数：
		sem_t sem;	定义类型。
	
		int sem_init(sem_t *sem, int pshared, unsigned int value);
	
		参数：
			sem： 信号量 
	
			pshared：	0： 用于线程间同步
					
					1： 用于进程间同步
	
			value：N值。（指定同时访问的线程数）


		sem_destroy();
	
		sem_wait();		一次调用，做一次-- 操作， 当信号量的值为 0 时，再次 -- 就会阻塞。 （对比 pthread_mutex_lock）
	
		sem_post();		一次调用，做一次++ 操作. 当信号量的值为 N 时, 再次 ++ 就会阻塞。（对比 pthread_mutex_unlock）
![pthread_cond_wait函数](pthread_cond_wait函数.png)

![读写锁](读写锁.png)

![互斥量](互斥量.png)

![死锁](死锁.png)

![锁的使用注意事项](锁的使用注意事项.png)

![条件变量实现的生产者消费者](条件变量实现的生产者消费者.png)

![线程同步和锁](线程同步和锁.png)

![信号量](信号量.png)

[pthread_sync_test](pthread_sync_test)
