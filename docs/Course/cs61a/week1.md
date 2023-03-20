# CS 61A FALL 2022

## 前期资料收集（10/26开始）

这门课是[SICP](https://link.zhihu.com/?target=http%3A//mitpress.mit.edu/sicp/)的变种，使用Python 3来展示抽象方法、编程范式和管理大型程序的技术。

CS61A 对应的教材是《计算机程序的构造和解释（SICP）》 ，核心思想是抽象，主要讲的是：

1. 编程范式——包括函数式编程(FP)、面向对象的编程(OOP)、结构化查询语言(SQL)；
2. 如何对一个问题拆分和程序实现（这个很关键）；
3. 也教了一点编译原理的内容——写个scheme 解释器。

千言万语难以表达我对这门课的喜爱和对UCB, Dr. John Denero, Dr. Hany Faird的感谢。就以他们的人生建议结束吧。

> When I was getting married, I was a PhD student at the time. My mom pulled me aside on my wedding day and said "John I want to give you some advice". I was like oh she's going to like tell me to listen to my wife or whatever. But she didn't. She said only two words that have stuck with me for a long time. She said "don't compare". That's all. And then she was like okay you can go back to do whatever you're doing. At the time this was very hard for me to process because I was in a university which is all about comparing people based on like what their exam score was. It turns out that out there in the world, there are no exams that everybody takes that are standardized anymore. All that matter is what you go and get done on your own particular path. So, comparing yourselves to other people becomes meaningless rapidly as what really matter is what you could do yourself, like what you're capable of and what you bother to do and how you choose to spend your time. It took years of this two-word phrase "don't compare" to marinate inside of me and for me to realize that my self-worth really has nothing to do with what other people can do or whether I can do it better than them or worse than them. It has everything to do with what i've done and what i'm gonna do next and how I spend my time and better myself. I should just focus on improving myself and forget about what everybody else is doing. (John Denero)
> It is something that took me a long time in life to understand not to compare. And there's a trap too that we do. We compare for example how big our house is to that one friend and how much money we make to another friend, and the kind of clothes we have to this friend and how smart we are to that friend. We pick and choose these things and that's first of all, even doing that individually is meaningless right? But it's also a trap and this is the problem with social media, you see these sore of curated worlds of other people and it's a trap. One of the great things of getting older is you will get there, I promise, you will realize it's a trap and comparing means absolutely nothing. It really is a very internal thing of what are you doing, who do you want to be, how do you want to go through this world, how do you want to treat other people. At the end of the day, that, and almost nothing else, is going to matter. And you got to just trust that it's going to be there. (Hany Faird)

学习顺序：基本上是按照reading-playlist（lecture）-lab-disc-hw-q&a-project，按照每天的任务依次完成即可。

官方的solutions会在作业截止后公布，但是因为几乎每学期的作业都差不多，所以在课程结束后会全部下架。因此如果是跟最新的课建议每次的solutions先保存下来，如果是学以前的可以找找网上的资源（笔者有部分20fa和21fa的）官方的答案还是非常值得看的，写的非常简洁，值得我们好好借鉴学习。

reading是最精华的部分，可以看出教授改编经典教材是下了心思的。lecture可以用作补充，会有具体的代码示例，同时也会补充一些reading里没有的东西，而Q&A更多的是讨论上课/作业/往年考试的一些问题，也经常讨论一些有意思的话题。笔者记得在第六次课时Q&A下面已经有时间戳了，选择自己想看的问题即可。

参考代码：

https://github.com/HobbitQia/CS61A-Fall-2020

https://github.com/311zzb/cs61a_fall2020





## Week 1

### Lecture 1

An introduction to computer science!

> A course about managing complexity, mastering abstraction, programming paradigms. 

computer science includes systems, artificial intelligence, graphics, security, networking, programming languages, theory and scientific computing.



> Learning happens when you don't solve the problem, when you are struggling through. When you solved the problem, you've learned it. It's over, right? 
>
> So the process of failure, the process of struggling, the process of taking hours to solve something is where the learning is happening.
>
> If somebody shortcuts that for you, or you shortcut that for somebody, you've cheated them.
>
> You've cheated and you've cheated them.
>
> And so don't be frustrated by things not working, that's the way it's supposed to be. That's what the process of learning is and it's okay

`Build good habits`



lab: the most important part of this course

Lecture -> Q&A -> lab intro -> finish the lab -> try the homework -> lecture -> discussion intro -> tutorials -> finish the homework -> lecture Q&A

Lab 1h

3 programming languages: python, scheme, SQL





### chapter 1.1 programming in python

> And, as imagination bodies forth
>
> The forms of things to unknown, and the poet's pen
>
> Turns them to shapes, and gives to airy nothing
>
> A local habitation and a name      ---William Shakespeare, A Midsummer-Night's Dream

> 想象会把不知名的事物用一种形式呈现出来，
>
> 诗人的笔再使它们有如实的形象，
>
> 空虚的无物也会有了居处和名字

*Structure and Interpretation of Computer Programs* (SICP)

Python excels as an instructional language

*prompt*, >>>

press <Control>-P (previous) and <Control>-N (next). <Control>-D exits a session

```python
from urllib.request import urlopen
shakespeare = urlopen("http://composingprograms.com/shakespeare.txt")
words = set(shakespeare.read().decode().split()) 
{w for w in words if len(w) == 6 and w[::-1] in words}
```









### lab00

使用exit()或者control+d退出到命令行界面

shell中文件名带有空格的处理办法：

```shell
cd Desktop/CS\ Notebook
```



```python
mkdir # 新建一个文件夹
mv ~/Downloads/lab00 ~/Desktop/cs61a/lab # 移动文件夹
cd # change into the specific direcory
```

Numbers may be combined with mathematical operators to form compound expressions. In addition to the `+` operator (addition), the `-` operator (subtraction), the `*` operator (multiplication) and the `**` operator (exponentiation), there are three division-like operators to remember:

- Floating point division (`/`): divides the first number number by the second, evaluating to a number with a decimal point *even if the numbers divide evenly*.
- Floor division (`//`): divides the first number by the second and then rounds down, evaluating to an integer.
- Modulo (`%`): evaluates to the positive remainder left over from division.

Floating point division (/) 得到浮点数，即使是整除

Floor division (//) 向下取整数，得到的是int

% 得到正整余数

```python
>>> 7 / 4
1.75
>>> (2 + 6) / 4
2.0
>>> 7 // 4        # Floor division (rounding down)
1
>>> 7 % 4         # Modulus (remainder of 7 // 4)
3

```



比如：

```
-7 % 5 = 3
原因在于-7 = 5 * （-2）+ 3
```



在python interpreter 中，变量的值等于最后一个等号后的值。

比如：

```
>>> y = 5
>>> y = y + 3
>>> y * 2

y *2结束后，terminal中返回的是16；y*2只是进行了计算，并没有改变y的值
但是现在y的值仍然是8
```



The lines in the triple-quotes `"""` are called a **docstring**

The lines that begin with `>>>` are called **doctests**



##### OK autograder commands

```shell
python3 OK
python3 ok --submit // Could not submit: Late Submission of cal/cs61a/fa20/lab00
```



- **`-i`**: The `-i` option runs your Python script, then opens an interactive session. In an interactive session, you run Python code line by line and get immediate feedback instead of running an entire file all at once. To exit, type `exit()` into the interpreter prompt. You can also use the keyboard shortcut `Ctrl-D` on Linux/Mac machines or `Ctrl-Z Enter` on Windows.

  If you edit the Python file while running it interactively, you will need to exit and restart the interpreter in order for those changes to take effect.

  ```shell
  python3 -i 
  ```

- **`-m doctest`**: Runs doctests in a particular file. Doctests are surrounded by triple quotes (`"""`) within functions.

  Each test in the file consists of `>>>` followed by some Python code and the expected output (though the `>>>` are not seen in the output of the doctest command).

  ```shell
   python3 -m doctest 
  ```



### chapter 1.2 elements of programming

every powerful language has 3 mechanisms:

- Primitive expressions and statements -- represent the simplest building blocks that the language provides
- Means of combination -- by which compound elements are built from simpler ones
- Means of abstraction -- by which compound elements can be named and manipulated as units

In programming, we deal with functions and data

`max(7.5, 9.5)` operator(operand, operand)

we say that the function max is called with arguments 7.5 and 9.5, returns a value of 9.5\

`pow()`raises its first argument to the power of its argument



The `=` symbol is called the *assignment* operator in Python (and many other languages). Assignment is our simplest means of *abstraction*, for it allows us to use simple names to refer to the results of compound operations, such as the `area` computed above. In this way, complex programs are constructed by building, step by step, computational objects of increasing complexity.



The possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an *environment*.



### Lecture 2

operand subexpression


 Evaluation procedure for call expressions:

1. Evaluate the operator and then the operand subexpressions 
2. Apply the function that is the value of the operator to the arguments that are the values of the operands

















































