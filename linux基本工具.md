# 1. vi
### 进入输入模式方法标
1. a 光标后输入
2. A 行末输入
3. i 光标前输入
4. I 行首输入
5. o 行前插入
6. O 行尾输入

### 特殊字符
1. gg 移动到文档起始位置
2. 0 移动到行首
3. ^ 移动行首第一个可见字符
4. $ 移动到行尾
5. G 移到文件最后一行
6. nG 移动到第n行
7. 移动光标
    h:左
    k:上
    j:下
    l:右
    
### 删除
1. x删除光标字符
2. X删除光标前字符
3. dd删除当前行
4. 10dd删除10行

### 复制
1. [n]yy复制一行或n行
2. p粘贴    

### 修改
1. s修改光标字符
2. r替换光标字符

### 重复
1. nx 删除n个字符
2. ndd 删除n行
3. ns 修改n个字符

### 取消前一动作
1. u 撤销上一指令
2. U 撤销本行上的所有修改

### 查找字符
1. /字符串:光标处向后查找字符串
2. ?字符串:光标处向前查找字符串
3. n:光标向后找下一个字符串

### 查看编辑状态
< Ctrl >+g 显示正在编辑的文件名、当前光标所在行数、文件总行数、文件是否被修改
### 括号匹配
% 定位到匹配（），{}
### 标记

1. ma(当前行) y'a(移动到其他行):块复制，p把块复制的内容粘贴在当前行下面
2. ma d'a 块删除
### 环境设置
:set nu 显示行号
:set ts=n 设置TAB长度 n
:syntax on 语法高亮显示

#### 下面是个人常使用的命令，列出来供大家参考。
1. 熟练掌握a（append）表示追加，i(insert)表示插入，o(open)表示向下插入空行。
2. 知道^表示行的第一个字符，0表示行首，$表示行末，w（word）表示单词，数字表示范围，\表示转义字符，gg表示文件头，G表示文件尾。
3. 知道d（delete）表示删除，y（yank）表示复制，p（paste）表示粘贴，c（change）表示修改，v（visual）表示可视化，=表示排版，.表示重复，m（mark）表示标记。
4. 知道x表示删除一个字符，r表示修改一个字符，s表示替换一
个字符，9s表示替换9个字符，直到按Esc键结束替换。
5. 熟练掌握末行替换命令s的用法，知道数字是表
示范围和可以使用正则表达式。知道末行模式“!+命令”是执行外部命令，“命令+!”是执行强制命
令。
6. 知道用w可以把当前文件写入到另一个文件，用r可以读取指定文件内容到当前光标下一行。
7. 知道用/、?、n命令查找特定字符串。
8. 知道u表示撤销，知道可以用标记操作m（mark）来完成块复制和块删除。
9. 知道^[表示Esc键，^M表示回车

---
### 组合命令示意
命令字符|特殊标识字符|组合指令|含义
--|--|--|--
d|10|10dd|删除10行
d|2|dw|删除单词
d|^|d^|删除到文件头
d|$|d$|删除到行尾
c|w|cw|修改单词
c|w、10|10cw|修改10个单词
c|0|c0|修改到文件头
c|$|c$|修改到文件尾
y|10|10yy p|复制10行然后用p粘贴
y|w|yw|复制单词
y|0|y0|复制到行首
y|$|y$|复制到行尾
m、y| |ma y'a p|块复制
m、d| |ma d'a|块删除
***
# 2. gcc
---
### gcc支持的文件格式
文件后缀|文件说明|文件后缀|文件说明
--|--|--|--
.c|C源文件|.C,.cc,.cxx,.cpp|C++ 源文件
.m|Ojective C文件|.h|预处理文件
.i|预处理后的C文件|.ii|预处理后的C++ 文件
.s|汇编语言源程序|.S|汇编语言源程序
.o|目标文件|.a|归档库文件
---
### gcc常用选项列表
选项|解释
--|--
-ansi|只支持ANSI标准的C语法。这一选项将禁止GNU C的某些特色，如asm或typedef 关键字词
-c|只编译并生成目标文件
-DMACRO|以字符串"1"定义宏MACRO
-DMACRO=DEFN|以字符串"DEFN"定义的MACRO
-E|只运行C预编译
-g|生成调试信息
-IDIRECTORY|指定额外的头文件搜索路径DIRECTORY
-LDIRECTORY|指定额外的函数库搜索路径DIRECTORY
-ILIBRARY|链接是搜索指定的函数库LIBRARY
-o FILE|生成指定的输出文件，用来生成名称为FILE的可执行文件
-O0|不优化
-O或-O1|优化生成代码
-O2|进一步优化
-O3|比-O2更进一步优化
-shared|此选项表明尽量使用动态链接库
-static|禁止使用动态链接库
-UMACRO|取消MACRO宏的定义
-w|不生成任何警告信息
-Wall|生成所有警告信息
---
# 3. makefile
---
### 返回值
值|解释
--|--
0|成功
1|错误
2|如果使用了-q选项，并且一些目标不需要更新返回2
### @作用
    不显示此命令行
### TAB
    命令行开始
## 命令行开头的[-]
    无论命令是否错误，都认为成功
```makefile    
    clean:
      -rm -rf *.o    
```        
---
变量的四种定义方式
1. 使用=或define来定义，这种方式下，前面变量使用后面的变量时，Makefile推导时会自动先对后面变量进行赋值之后，再对前面的变量进行赋值。
2. 使用:=号定义变量，这种方式下前面，变量使用后面的变量时，后面的变量在当前使用时为空值。
3. 使用+=对变量追加内容。
4. 使用?=对变量进行定义，如果前面变量未定义则定义，否则什么也不做
---
### makefile符号预定义
变量|含义说明
--|--
$+|所有的依赖文件，以空格分开，并以出现的先后为序，可能包含重复的依赖文件
$?|所有依赖文件，以空格分开，这些依赖文件的修改日期比目标的创建日期晚
$^|所有的依赖文件，以空格分开，不包含重复的依赖文件
$@|目标的完整名称
$<|第一个依赖文件的名称
$%|仅当目标是归档成员（函数库文件）时，该变量表示目标的归档成员名称。例如，如果目标名称为mytarget.so(image.o)，则$@为mytarget.so,而$%为image.o。如果目标不是归档成员,此值为空
---
### 与编译相关的预定义变量
变量名称|含义说明
--|--
AR|归档维护程序的名称，默认值ar
ARFLAGS|归档维护程序的选项
AS|汇编程序的名称，默认as
ASFLAGS|汇编程序的选项
CC|C编译器的名称，默认cc
CCFLAGS|C编译器的选项
CPP|C预编译的名称，默认值$(CC) -E
CPPFLAGS|C 预编译器的选项
CXX|C++编译器的名称，默认值g++
CXXFLAGS|C++ 编译器的选项
---
### Makefile命令行选项
名称|含义
--|--
-C DIR|在读取makefile之前该变到指定的目录DIR
-f FILE|以指定的FILE文件作为makefile
-h|显示所有的make选项
-i|忽略所有的命令执行错误
-I DIR|当包含其他makefile文件，可利用该选项指定搜索目录
-n|只打印要执行的命令，但不执行这些命令
-p|显示make变量数据库和隐含规则
-s|在执行命令是不显示命令
-w|在处理makefile之前和之后，显示工作目录
-W FILE|假定文件FILE已经被修改
---
1. 使用“=”对变量进行赋值时，first变量使用后面second变量，second变量先进行赋值，然后再对first进行赋值。
2. 使用“：=”对变量赋值时，sunday变量使用后面的monday变量，monday变量对sunday变量不起作用（其值为空）。
3. 使用“?=”对变量进行赋值时，sky变量进行了两次定义，但只有第一次的定义有效。
4. 使用“+=”对变量进行赋值时，xobj变量对原有内容保留，对新的赋值进行了
---
# 4. gdb
---
### gdb命令
---
>Makefile的后缀规则，必须首先由.SUFFIXES来进行声明支持后缀的类型，如.SUFFIXES：.sqc .c。 后缀规则（Suffix Rule）是定义隐含规则的老风格方法。后缀规则定义将一个具有某个后缀的文件（如.c文件）转换为具有另外一种后缀的文件（如.o文件）的方法。每个后缀规则以两个成对出现的后缀名定义，如将“.c”文件转换为“.o”文件的后缀规则可定义如下：
```makefile
 .c.o: $(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@
```

---
gdb命令|说明
--|--
backtrace|显示程序中的当前位置和表示如何到达当前位置的栈跟踪，可以简写bt
breakpoint|在程序中设置一个断电
cd|改变当前工作目录
clear|删除刚才停止处的断点
commands|命中断点时，列出将要执行的命令
continue|从断点开始继续执行
delete|删除一个断点或监测点。也可以与其他命令一起使用
display|显示变量或表达式
down|下移栈帧，使得另一个函数成为当前函数
frame|选择下一条continue命令的帧
info|显示与程序相关的各种信息
jump|在源程序中的另一点开始运行。
kill|异常中止在gdp
list|列出相应于正在执行的程序的源文件内容
next|执行下一个源程序行，从而执行其整体中的一个函数
print|显示变量或表达式的值
pwd|显示当前工作目录
quit|退出gdb
reverse-search|在源文件中方向搜索正则表达式
run|执行该程序
search|在源文件中搜索正则表达式
set variable|给变量赋值
signal|将一个信号发送到正在运行的进程
step|执行下一个源程序行，必要时进入下一个函数
undisplay|display命令的反命令，不要显示表达式
until|结束当前循环
up|上移栈帧，使另一函数成为当前函数
watch|在程序中设置一个监测点（即数据断点）
whatis|显示变量或函数类型
where|打印所有堆栈帧的栈信息
---
### gdb 常用命令

gdb命令|说明
--|--
break NUM|在指定行上设置断点
clear|删除设置在特定源文件、特定行上的断点。clear FILE:NUM
continue|继续执行正在调试的程序
display EXPR|每次程序停止后，显示表达式的值
file FILE|装载指定的可执行文件进行调试
help NAME|显示指定命令的帮助信息
info break|显示当前断点清单，包括到达断点处的次数等
info files|显示被调试文件的详细信息
info func|显示所有的函数名称
info local|显示当前函数中的局部变量信息
info prog|显示被调试程序的执行状态
info var|显示所有的全局和静态变量名称
kill|终止正被调试的程序
list|显示源代码段
make|在不退出提示符的情况下编译源代码
next|在不单步执行进入其他函数的情况下，向前执行一行源代码
print EXPR|显示表达式
---
#### break命令（可以简写为b）可以用来在调试的程序中设置断点。 该命令有如下四种形式：
1. break linenumber，使程序恰好在执行给定行之前停止。
2. break function-name，使程序恰好在进入指定的函数之前停止。
3. break line-or-function if condition，如果condition（条件）是真，程序到达指定行或函数时停止。
4. break routine-name：在指定例程的入口处设置断点。 如果该程序是由很多源文件构成的，可以在各个源文件中设置断点，而不是在当前的源文件中设置断点，其方法如下：
```shell
(gdb) break filename:line-number
(gdb) break filename:function-
```
---
#### 单步执行的相关命令如下：
1. next：不进入函数的单步执行。
2. step：进入函数的单步执行。
3. 如果已经进入了某函数，当想退出该函数返回到它的调用函数中时，可使用命令

----
# 5. daemon 进程

1. fork创建子进程后，父进程调用exit退出，子进程脱离Shell
2. 调用setsid 建立新会话，成为首进程
3. 再次调用fork 建立子进程
4. chdir改变当前目录
5. 重设文件权限掩码umask(0)
6. 关闭0,1,2文件描述符
7. 重定向0,1,2
8. 处理SIGCHLD:signal(SIGCHLD,SIG_IGN);

## Code
``` C
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include <fcntl.h>
    #include <sys/types.h>
    #include <unistd.h>
    #include <sys/wait.h>
    #define MAXFILE 512
    int main(){
       pid_t pc;
       int i,fd,len;
       int j;
       pc=fork();
       if(pc<0){
           printf("error fork\n");
           exit(1);
       }else if(pc>0){
           exit(0);
       }
       setsid();
       pc=fork();
       if(pc<0){
           printf("error fork\n");
           exit(1);
       }else if(pc>0){
           exit(0);
       }
       chdir("/");
       umask(0);
       for(i=0;i<MAXFILE;i++)
           close(i);
       j=open("/dev/null",O_RDWR);
       dup2(j,0);
       dup2(j,1);
       dup2(j,2);
       signal(SIGCHLD,SIG_IGN);
       while(1){
            sleep(3);
       }
       return 0;
    }
```
---
# 6. process 进程
### 建立进程
1. fork
2. exec
    * execl(const char* path,const char* arg,...)
    * execlp(const char* file,const char* arg,...)
    * execle(const char* path,const char* arg,...,char* const envp[]);
    * execv
    * execvp
    * execve
> path:为路径，file:可执行文件名
---
### 进程同步
1. pid_t wait(int* status);等待直到子进程僵尸状态
``` C
    w=wait(&status)
    if(WIFEXITED(status))
        printf("process ret=%d\n",WEXITSTATUS(status));
```
2. pid_t waitpid(pid_t pid,int* status,int options);
    1. pid=0,等待所有子进程
    2. options:
      * WNOHANG:子进程没有关闭也返回
      * WUNTRACED:如果子进程暂停执行也返回

### fg bg
  1. bg:进程放入后台
  2. fg 1
    * 1:作业编号

### jobs
  1. < Ctrl >+Z ：显示作业编号
  2. jobs 查看作业列表

### 信号
1. sigemptyset
2. sigfillset
3. sigaddset
4. sigdelset
5. sigismember
6. sigprocmask
7. sigpending

### 信号捕获
1. signal
2. sigaction
3.sigsuspend

### 管道
1. pipe：匿名管道
2. popen/pclose
3. mkfifo,open,read,write,close 命名管道

### 消息队列
1. msgget
2. msgsnd
3. msgrcv
4. msgctl

### 信号量
1. semget
2. semctl
3. semop

### 共享内存
1. shmget
2. shmat
3. shmdt
4. shmctl


# 7. pthread
>-lpthread

### 线程函数
1. pthread_create
2. pthread_self：线程ID
3. pthread_exit：线程退出
4. pthread_cancel：终止
5. pthread_join：挂起
6. pthread_detach:分离
### 线程属性
    1. pthread_attr_init
    2. pthread_attr_destroy

### 线程的分离状态
    1. pthread_attr_setdetachstate
    2. pthread_attr_getdetachstate

### 调度策略
    1. pthread_attr_setschepolicy
    2. pthread_attr_getschepolicy

### 线程的调度参数
    1. pthread_attr_setscheparam
    2. pthread_attr_getscheparam
### 线程的继承性
    1. pthread_attr_setinheritsched
    2. pthread_attr_getinheritsched
### 线程的作用域
    1. pthread_attr_setscope
    2. pthread_attr_getscope
### 线程的栈
1. pthread_attr_setstacksize
2. pthread_attr_getstacksize
3. pthread_attr_setstackaddr
4. pthread_attr_getstackaddr
5. pthread_attr_setstack
6. pthread_attr_getstack

### 线程同步
1. 互斥锁
    - pthread_mutex_init
    - pthread_mutex_lock
    - pthread_mutex_unlock
    - pthread_mutex_destroy
    - pthread_mutex_trylock
    - pthread_mutex_t mutex=PTHREAD_MUTEX_INITIALIZER
2. 条件变量
    - pthread_cond_init
    - pthread_cond_wait
    - pthread_cond_timedwait
    - pthread_cond_signal
    - pthread_cond_broadcast
    - pthread_cond_destroy
    - pthread_cond_t cond=PTHREAD_COND_INITIALIZER
3. 信号量
    - sem_init
    - sem_wait
    - sem_post
    - sem_destroy
    - sem_getvalue
