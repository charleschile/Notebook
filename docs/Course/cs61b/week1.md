# CS61B week1

学习的顺序：Reading（精华的课程内容）-> Guide （课程内容的总结）-> Slides + Video -> Lab -> HW -> project

entry code: 93PK75



lab1 setup就是教了一下怎么配置自己的电脑，用来跑java

```bash
cd . 回到现在这个文件夹，相当于什么都没做
cd .. 回到parent文件夹
ls -l 会把读写状态都给显示出来
mkdir 新建文件夹
cp 复制一个文件
mv 移动一个文件
open . 是打开file explorer在现在的文件夹
rm -r
```

println包含了一个新的行

Java有static typing, a key feature of Java compiler is that it performs a static type check.

出现类型错误的话，compiler会拒绝运行

python是dynamically typed language

Java可以`System.out.println(5 + " ");`也可以`String h = 5 + "horse";`

但是python不可以`print(5 + "horse")`，因为python doesn't know what the statement is supposed to be, a number or a string?



As an analogy, programming in Python can be a bit like [Dan Osman free-soloing Lover's Leap](https://www.youtube.com/watch?v=NCByLWtM7y4). It can be very fast, but dangerous. Java, by contrast is more like using ropes, helmets, etc. as in [this video](https://www.youtube.com/watch?v=tr6UIfPEuI0).







### Exercise

```java
public class HelloNumbers {
    public static void main (String[] args) {
        int x = 0;
        int sum = 0;
        while (x < 10) {
            System.out.println(sum);
            x = x + 1;
            sum = sum + x;
        }
    }
}
```



