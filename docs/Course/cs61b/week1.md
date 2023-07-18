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

#### comment

In a Javadoc comment, the block comment starts with an extra asterisk, e.g. `/**`, and the comment often (but not always) contains descriptive tags. 

#### 定义array

```java
public class HelloNumbers {
    public static void main(String[] args){
        int[] numbers = new int[]{1, 3, 5, 7};
        System.out.println(numbers[3]);
        System.out.println(numbers.length);
    }
}
```

#### continue和break

解释是`continue`可以直接跳过现在所在的这个循环，进入到下一个i的自增循环

The `continue` statement skips the current iteration of the loop, effectively jumping straight to the increment condition.

而`break`是直接终止包含这个`break`的最内层的循环

By contrast, the `break` keyword completely terminates the innermost loop when it is called. 

```java
public class HelloNumbers {
    public static void main (String[] args) {
        String[] a = {"cat", "horse", "dog", "elephant"};
        for (int i = 0; i < a.length; i += 1) {
            if (a[i].contains("horse")) {
                continue;
            }
            for (int j = 0; j < 3; j += 1) {
                System.out.println(a[i]);
            }
        }
    }
}
```

​	输出是：

```bash
cat
cat
cat
dog
dog
dog
elephant
elephant
elephant
```

而将`continue`改成`break`之后，那么会输出：

 ```bash
 cat
 cat
 cat
 ```



另外一个`break`的例子：

```java
public class HelloNumbers {
    public static void main(String[] args) {
        String[] a = {"cat", "dog", "laser horse", "ketchup", "horse", "horbse"};

        for (int i = 0; i < a.length; i += 1) {
            for (int j = 0; j < 3; j += 1) {
                System.out.println(a[i]);
                if (a[i].contains("horse")) {
                    break;
                }
            }
        }
    }
}
```

输出：

```bash
cat
cat
cat
dog
dog
dog
laser horse
ketchup
ketchup
ketchup
horse
horbse
horbse
horbse
```

在这个例子里面，`horse`和`laser horse`都只输出了一次，然后内层的循环就直接被终止了



### 增强for循环(enhanced for loop)

```java
public class EnhancedForBreakDemo {
    public static void main(String[] args) {
        String[] a = {"cat", "dog", "laser horse", "ketchup", "horse", "horbse"};

        for (String s : a) {
            for (int j = 0; j < 3; j += 1) {
                System.out.println(s);
                if (s.contains("horse")) {
                    break;
                }                
            }
        }
    }
}
```

输出是

```bash
cat
cat
cat
dog
dog
dog
laser horse
ketchup
ketchup
ketchup
horse
horbse
horbse
horbse
```









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



### Homework exercise 2

```java
public class Max {
    public static int max (int[] array) {
        int x = 0;
        int m = array[0];
        int length = array.length;
        while (x < length) {
            if (array[x]> m ) {
                m = array[x];
            }
            x = x + 1;
        }
        return m;
    }
    public static void main (String[] args) {
        int[] numbers = new int[]{9, 2, 15, 2, 22, 10, 6};
        System.out.println(max(numbers));
    }
}
```



### Homework exercise 4

```java
public class WindowPosSum {
	public static void windowPosSum(int[] a, int n) {
		/**
		 * replace each element a[i] with the sum of a[i] through a[i + n]
		 */
		// copy the a array to a new array b
		int[] b = new int[a.length];
		for (int i = 0; i < a.length; i += 1) {
			b[i] = a[i];
		}
		// 遍历每个元素
		for (int i = 0; i < a.length; i += 1) {
			if (a[i] <= 0) {
				continue;
			}
			else {
				if ((i + n) < a.length) {
					int temp = 0;
					for (int j = i; j <= i + n; j += 1) {
						temp += b[j];
					}
					a[i] = temp;
				}
				else {
					int temp = 0;
					for (int j = i; j < a.length; j += 1) {
						temp += b[j];
					}
					a[i] = temp;
				}
			}
		}
	}
	public static void main(String[] args) {
		int[] a = {1, 2, -3, 4, 5, 4};
		int n = 3;
		windowPosSum(a, n);
		System.out.println(java.util.Arrays.toString(a));
	}

}
```

### 使用break:

```java
public class WindowPosSum {
	public static void windowPosSum(int[] a, int n) {
		/**
		 * replace each element a[i] with the sum of a[i] through a[i + n]
		 */
		// copy the a array to a new array b
		int[] b = new int[a.length];
		for (int i = 0; i < a.length; i += 1) {
			b[i] = a[i];
		}
		// 遍历每个元素
		for (int i = 0; i < a.length; i += 1) {
			if (a[i] <= 0) {
				continue;
			}
			else {
				int temp = 0;
				for (int j = i; j <= i + n; j++) {
					if (j >= a.length) {
						break;
					}
					temp += b[j];
				}
				a[i] = temp;
			}
		}
	}
	public static void main(String[] args) {
		int[] a = {1, 2, -3, 4, 5, 4};
		int n = 3;
		windowPosSum(a, n);
		System.out.println(java.util.Arrays.toString(a));
	}

}
```

