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

### Lecture 1-Wed Welcome

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







### Lecture 1-Fri Functions

 notation

all expressions can use functions call notation

raise 6 to 3rd power:

```python
6 ** 3

from operator import add, mul
```



Add(2,3)

Operator: add

Operand subexpressions: 2, 3



从最里面到最外面，分别evaluate，这个过程叫做evaluation procedure

##### names, assignment, and user-defined functions

```
from math import pi, sin

```



Primitive expressions: 2, add, 'hello'

call expression: max(2, 3,) 由operator和oprand组成



##### Environment diagrams

Visualize the interpreter's process

code on the left,  and fames on the right



execution rule of assignment statements:

1. Evaluate all expressions to the right of = from left to right
2. Bind all names to the left of = to the resulting values in the current frame

Current frame这意味着：

```python
a = 1
b = 2
b, a = a + b, b // b = 3, a = 2
//而如下会导致:
b = a + b
a = b // a = 3
```

##### defining functions

The assignment is a simple means of abstraction: binds names to values

The function definition is a more powerful means of abstraction: binds names to expressions

Indent 缩进

```python
def <name> (<formal parameters>): // function signature
  return <return expression> // function body
```



an environment is a sequence of frames

 ```python
 >>> def square(square):
 ...     return mul(square, square)
 ...
 >>> square(4)
 16
 ```

注意先在local frame里面找，然后再到global frame中去找





### Hw01 variables & functions, control

To check if `b` evenly divides `a`, you can use the expression `a % b == 0`, which can be read as, "the remainder of dividing `a` by `b` is 0."



##### non-pure functions

Print() is non-pure function that can generate side effects

```python
>>> print(print(1), print(2))
1
2
None None
```

Be careful with `print`! The fact that it returns `None` means that it *should not* be the expression in an assignment statement.

pure functions are essential for writing *concurrent* programs

## Week 2



### Lecture 2

operand subexpression


 Evaluation procedure for call expressions:

1. Evaluate the operator and then the operand subexpressions 
2. Apply the function that is the value of the operator to the arguments that are the values of the operands



### Chapter 1.4

domain 输入值的变化范围

range 输出值的值域



the qualities of good functions all reinforce the idea that functions are abstractions

定义函数以及它的doctoring：

```python
>>> def pressure(v, t, n):
        """Compute the pressure in pascals of an ideal gas.

        Applies the ideal gas law: http://en.wikipedia.org/wiki/Ideal_gas_law

        v -- volume of gas, in cubic meters
        t -- absolute temperature in degrees kelvin
        n -- particles of gas
        """
        k = 1.38e-23  # Boltzmann's constant
        return n * k * t / v
      
  >>> help(pressure)
```





可以直接在定义函数的时候设定n的默认值(indicate its default value)： 

```python
def pressure(v, t, n=6.022e23):
```

如果使用默认值的话，在输入的时候可以只输入两个变量：

```python
>>> pressure(1, 273.15)
2269.974834
```





### Chpater 1.5 Control

Rather than being evaluated, statements are *executed*. 

we have seen three kinds of statements already: assignment, `def`, and `return` **statements**



A statement is executed by the interpreter to perform an action




conditional statements execute the suite annd skip the remaining 



##### Boolean contexts

False values in Python: False, 0, '', None

True values in Python: anything else(True)



##### statement 和expression的区别

statements are instructions that perform some action, while expressions are units of code that evaluate to a value.

A statement is a line of code that performs some action, such as assigning a value to a variable, calling a function, or looping over a sequence. Statements are typically terminated by a newline character, although semicolons can be used to separate multiple statements on a single line.

For example, the following are examples of statements in Python:

```python
x = 5             # assign a value to x
print("hello")    # call the print function
while x > 0:      # loop while x is greater than 0
    x -= 1
```



On the other hand, an expression is a combination of values, variables, and operators that evaluates to a single value. Expressions can be used as part of a larger statement, or they can be used on their own to return a value.

For example, the following are examples of expressions in Python:

```python
3 + 4             # evaluates to 7
x + 2             # evaluates to the value of x plus 2
len("hello")      # evaluates to 5 (the length of the string)

```

##### short-circuting

In Python, short-circuiting is a behavior exhibited by logical operators (i.e. "and" and "or") where the second operand is not evaluated if the result of the expression can be determined by evaluating the first operand alone.

例如，在表达式"a and b"中，如果"a"的值为False，那么不管"b"的值是多少，整个表达式都将为False。因此，不需要求“b”，Python将“短路”表达式的求值，节省时间和计算资源。

类似地，在表达式"a or b"中，如果"a"的值为True，那么不管"b"的值是多少，整个表达式都将为True。同样，不需要计算“b”，Python会缩短计算过程。



```python
1	def fib(n):
2	    """Compute the nth Fibonacci number, for n >= 2."""
3	    pred, curr = 0, 1   # Fibonacci numbers 1 and 2
4	    k = 2               # Which Fib number is curr?
5	    while k < n:
6	        pred, curr = curr, pred + curr
7	        k = k + 1
8	    return curr
9	
10	result = fib(8)
```

#### 1.5.6 tesing

##### assertions

```python
assert fib(8) == 13, 'The 8th Fibonacci number should be 13'
```

When writing Python in files, rather than directly into the interpreter, tests are typically written in the same file or a neighboring file with the suffix `_test.py`.

##### doctests

Python provides a convenient method for placing simple tests directly in the docstring of a function. The first line of a docstring should contain a one-line description of the function, followed by a blank line. A detailed description of arguments and behavior may follow. In addition, the docstring may include a sample interactive session that calls the function:

```python
def sum_naturals(n):
        """Return the sum of the first n natural numbers.

        >>> sum_naturals(10)
        55
        >>> sum_naturals(100)
        5050
        """
        total, k = 0, 1
        while k <= n:
            total, k = total + k, k + 1
        return total
```



`testmod()` is used to run tests in a module, while `run_docstring_examples()` is used to test a specific function or method.

Testmod()

```python
>>> from doctest import testmod
>>> testmod()
```

Run_docstring_examples

```python
>>> from doctest import run_docstring_examples
>>> run_docstring_examples(sum_naturals, globals(), True)
```

When writing Python in files, all doctests in a file can be run by starting Python with the doctest command line option:

这个命令不需要上面两个功能，可以在有doctests的情况下，直接用命令行使用，有错的话会报错，如果没有错就不会返回任何东西

```python
python3 -m doctest <python_source_file>
```



### lab01

这个是死循环：(python里面只有0是false)

```python
positive = 28
while positive: # If this loops forever, just type Infinite Loop
    print("positive?")
    positive -= 3
```

Python 的循环只有碰到0（相当于False）才会停下来



```python
>>> True and 13
>>> 13

>>> False or 0
>>> 0

>>> not 10
>>> False
-- OK! --

>>> not None
>>> True
```

python 里面使用and时，如果第一个数是错的，那么会直接返回第一个数；如果第一个数是对的，那么会返回第二个数；第二个数只有在第一个数是对的情况下才会被判断

> 理解：and是逻辑运算，如果第一个是错的，那么这个表达式就是错的，即返回第一个值；如果第一个数字是对的，那么这个表达式的值取决于第二个值：比如，第二个值如果是错误的，那么就返回错误（即第二个值）如果是正确的，也是返回第二个正确的值

而使用or的时候，如果第一个数是对的，那么直接返回第一个数；如果第一个数是错的，那么直接返回第二个数

OR是这要有一个数true就是true



In Python, the `and` and `or` operators are used to evaluate logical expressions.

The `and` operator returns the first operand if it evaluates to False, and the second operand otherwise. The second operand is only evaluated if the first operand is True. So, when we evaluate the expression `True and 13`, the first operand `True` is not False, so Python returns the second operand `13`.

The `or` operator returns the first operand if it evaluates to True, and the second operand otherwise. The second operand is only evaluated if the first operand is False. So, when we evaluate the expression `False or 0`, the first operand `False` is not True, so Python returns the second operand `0`.



`-v`is for verbose

```python
python3 -m doctest file.py -v
```



> cs 61a 里面print('DEBUG: result is', result)，以DEBUG开头的输出都会被ok autograder忽略





#### Debugging

##### running doctests

在statement里面写好doctests，然后可以assertion, Testmod(), Run_docstring_examples(), 或者命令行（可以去掉-v）:

```python
python3 -m doctest file.py -v
```

##### 使用print打点

```python
print('DEBUG: result is', result)
```

###### 使用flag作为long-term debugging的工具

```python
debug = True

def foo(n):
i = 0
while i < n:
    i += func(i)
    if debug:
        print('DEBUG: i is', i)
```

##### interative debugging (use of an interactive REPL)

```
python -i file.py
```

然后直接在命令行中输入类似:

```python
print(foo(2))
```

会直接返回foo(2)的值

##### assert

下面的语句用来直接确认输入的是整数：

```python
def double(x):
    assert isinstance(x, int), "The input to double(x) must be an integer"
    return 2 * x
```







