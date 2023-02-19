# MIT The Missing Semester of Your CS Education

## information

- 重点熟悉 `Git` `GitHub` `make` `gdb`/`lldb` `VS Code` `Markdown`



### Course overview + Shell

Shell: 它允许你执行程序，输入并获取某种半结构化的输出。

Bourne Again SHell, 简称 “bash” 



1. `date`

   它打印出了当前的日期和时间

   2023年 2月18日 星期六 10时37分36秒 CST

2. `echo hello`

   `echo` 程序将`hello`参数打印出来

   注意参数里面不应该有空格，如果您希望传递的参数中包含空格（例如一个名为 My Photos 的文件夹），您要么用使用单引号，双引号将其包裹起来，要么使用转义符号 `\` 进行处理（`My\ Photos`）。

   比如`echo Hello\ World`

   ```shell
   ➜  try mkdir My Photos
   ➜  try ls
   My     Photos
   ➜  try mkdir My\ Photos
   ➜  try ls
   My        My Photos Photos
   ```

   

3. Shell 指令搜索的路径

   ```shell
   ➜  ~ echo $PATH
   /Library/Frameworks/Python.framework/Versions/2.7/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin:/Library/Apple/usr/bin
   ➜  ~ which echo
   echo: shell built-in command
   ➜  ~ /bin/echo $PATH
   /Library/Frameworks/Python.framework/Versions/2.7/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin:/Library/Apple/usr/bin
   ```

   

4. 在shell中导航

   shell 中的路径是一组被分割的目录，在 Linux 和 macOS 上使用 `/` 分割，而在Windows上是 `\`。

   路径 `/` 代表的是系统的根目录，如果某个路径以 `/` 开头，那么它是一个 *绝对路径*，其他的都是 *相对路径* 。如果某个路径以 `/` 开头，那么它是一个 *绝对路径*，其他的都是 *相对路径* 。

   ```shell
   ➜  ~ pwd
   /Users/charleschile
   ➜  ~ cd /home
   ➜  /home pwd
   /home
   ➜  /home cd ..
   ➜  / pwd
   /
   ➜  / cd ./home
   ➜  /home pwd
   /home
   ➜  /home cd
   ➜  ~
   ```

5. 查看指定目录下包含哪些文件，我们使用 `ls` 命令

```shell
➜  Desktop ls
Codes                                     Personal File                             草稿.docx                                 截屏2023-02-16 17.39.05.png               关键词：.md
ICA.docx                                  blockchain.md                             草稿2.docx                                截屏2023-02-17 08.44.15.png
Male infertility as a window to health.md 毕设                                      截屏2023-02-15 11.48.28.png               交易记录.md
➜  Desktop ls -l
total 1248
drwxr-xr-x@  6 charleschile  staff     192  1 18 11:36 Codes
-rw-r--r--@  1 charleschile  staff  260007  2 16 18:56 ICA.docx
-rw-r--r--@  1 charleschile  staff    2292  2 17 01:13 Male infertility as a window to health.md
drwxrwxrwx  13 charleschile  staff     416  1 13 12:43 Personal File
-rw-r--r--@  1 charleschile  staff   13623  2  7 11:35 blockchain.md
drwxrwxrwx@ 15 charleschile  staff     480  2 17 08:44 毕设
-rw-r--r--@  1 charleschile  staff   15101  2 16 15:08 草稿.docx
-rw-r--r--@  1 charleschile  staff   13410  2 17 04:51 草稿2.docx
-rw-r--r--@  1 charleschile  staff   22919  2 15 11:48 截屏2023-02-15 11.48.28.png
-rw-r--r--@  1 charleschile  staff  105133  2 16 17:39 截屏2023-02-16 17.39.05.png
-rw-r--r--@  1 charleschile  staff  183011  2 17 08:44 截屏2023-02-17 08.44.15.png
-rw-r--r--@  1 charleschile  staff    1018  2 10 12:26 交易记录.md
-rw-r--r--@  1 charleschile  staff     828  1 26 23:10 关键词：.md
```

`ls -l`这个参数可以更加详细地列出目录下文件或文件夹的信息。首先，本行第一个字符 `d` 表示 `missing` 是一个目录。然后接下来的九个字符，每三个字符构成一组。 （`rwx`）. 它们分别代表了文件所有者（`missing`），用户组（`users`） 以及其他所有人具有的权限。其中 `-` 表示该用户不具备相应的权限。从上面的信息来看，只有文件所有者可以修改（`w`），`missing` 文件夹 （例如，添加或删除文件夹中的文件）。为了进入某个文件夹，用户需要具备该文件夹以及其父文件夹的“搜索”权限（以“可执行”：`x`）权限表示。为了列出它的包含的内容，用户必须对该文件夹具备读权限（`r`）。对于文件来说，权限的意义也是类似的。注意，`/bin` 目录下的程序在最后一组，即表示所有人的用户组中，均包含 `x` 权限，也就是说任何人都可以执行这些程序。

比如`drwxr-xr-x`代表这是一个文件夹，`rwx`代表文件夹的所有者能够读、写、搜索这个文件夹里的内容，`r-x`代表用户组只能读和搜索，下一个`r-x`代表其他所有人也只能读和搜索

6. 文件的移动和重命名

   实际上将文件在同一个目录下移动就相当于更改了文件名：

   ```shell
   mv test.md try.md
   //实际上将test.md 改名成了try.md
   ```

   文件移动文件夹并且改名：

   ```shell
   ➜  try mv try.md ../test/test.md
   ```

7. 拷贝文件

   ```shell
   ➜  test cp test.md try.md
   ```

   

8. 新建文件夹

   ```shell
   ➜  test mkdir test1
   ```

   

9. 展示程序的用户手册

   ```shell
   man ls
   
   ```
   
   
   
10. 使用`>`和`<`在程序之间创建连接
   ```shell
   ➜  test cat test.md
   test%
   ➜  test echo hello > test.md
   ➜  test cat test.md
   hello
   
   
   
   ➜  test cat < test.md
   hello
   ➜  test cat < test.md > test2.md
   ➜  test cat test2.md
   hello
   ```



使用`|`将一个程序的输出和另外一个程序的输入连接起来

`tail -n1`是取出最后一行的内容

   ```shell
   ➜  ~ ls -l /
   total 9
   drwxrwxr-x  35 root  admin  1120  2 16 13:53 Applications
   drwxr-xr-x  67 root  wheel  2144  1 14 08:34 Library
   drwxr-xr-x@  9 root  wheel   288 12  2 16:43 System
   drwxr-xr-x   5 root  admin   160 12  2 16:43 Users
   drwxr-xr-x   3 root  wheel    96  2 18 09:46 Volumes
   drwxr-xr-x@ 38 root  wheel  1216 12  2 16:43 bin
   drwxr-xr-x   2 root  wheel    64 12  2 16:43 cores
   dr-xr-xr-x   3 root  wheel  4430  2 18 09:46 dev
   lrwxr-xr-x@  1 root  wheel    11 12  2 16:43 etc -> private/etc
   lrwxr-xr-x   1 root  wheel    25  2 18 09:46 home -> /System/Volumes/Data/home
   drwxr-xr-x   2 root  wheel    64 12  2 16:43 opt
   drwxr-xr-x   6 root  wheel   192  2 18 09:46 private
   drwxr-xr-x@ 65 root  wheel  2080 12  2 16:43 sbin
   lrwxr-xr-x@  1 root  wheel    11 12  2 16:43 tmp -> private/tmp
   drwxr-xr-x@ 11 root  wheel   352 12  2 16:43 usr
   lrwxr-xr-x@  1 root  wheel    11 12  2 16:43 var -> private/var
   ➜  ~ ls -l / | tail -n1
   lrwxr-xr-x@  1 root  wheel    11 12  2 16:43 var -> private/var
   ```



### Shell Tools and Scripting

