# 一些小技巧

### tips

1. 输出一个整数的各位，直接`char str[n]`，然后输出即可，当成int处理反而麻烦

### C++ 中各种取整

```c++
// 引入头文件
#include <cmath>
#incldue <math.h>
floor() // 不大于自变量的最大整数
ceil() // 不小于自变量的最大整数
round() // 四舍五入
fix() // 向0取整
```







向上取整技巧：

```c++
// 注意C++里面/是向下取整，即9/4=2
#include <cmath>
ceil((double) 9 / 4) // 输出3
//或者使用（被除数 + 除数 - 1）/除数 = 向上取整
int res = (9 + 4 - 1) / 4 // 输出3
```






### 简单的双指针来将数组中的奇偶进行左右分类

```c++
// 双指针法将所有数进行奇偶排序，奇数在左边，偶数在右边
    int l = 0, r = 5;
    while (l < r) {
        bool leftIsOdd = num[l] % 2 == 1;
        bool rightIsEven = num[r] % 2 == 0;
        if (leftIsOdd) {
            l++;
        } else if (rightIsEven) {
            r--;
        } else if (!leftIsOdd & !rightIsEven) {
            int tmp = num[l];
            num[l] = num[r];
            num[r] = tmp;
        }
    }
```



### C++中绝对值

```cpp
#include <iostream> 中 abs() 对整数进行绝对值
#include <cmath> 中fabs() 对浮点型进行绝对值
```



### 质因数问题

tips：使用反证法易得，一个数a只会有一个大于`a^1/2的因数`，所以只需要讨论从2到`a^1/2`就行，然后再单独讨论1和大于根号a的情况，千万不要忘记大于根号a的那个数

质因数不包含1，因数包含1

#### AcWing 867. 分解质因数

给定 n 个正整数 ai，将每个数分解质因数，并按照质因数从小到大的顺序输出每个质因数的底数和指数。

#### 输入格式

第一行包含整数 n。

接下来 n 行，每行包含一个正整数 ai。

#### 输出格式

对于每个正整数 ai，按照从小到大的顺序输出其分解质因数后，每个质因数的底数和指数，每个底数和指数占一行。

每个正整数的质因数全部输出完毕后，输出一个空行。

#### 数据范围

1≤n≤100,
2≤ai≤2×109

####  输入样例：

```
2
6
8
```

#### 输出样例：

```
2 1
3 1

2 3
```

```c++
#include <iostream>
using namespace std;

int main () {
    int n;
    scanf("%d", &n);
    while (n--) {
        int a;
        scanf("%d", &a);
        for (int i = 2; i <= a/i; i++) {
            int e = 0;
            if (a % i != 0) continue;
            else {
                while (a % i == 0) {
                    e += 1;
                    a /= i;
                }
            }
            cout << i << ' ' << e << endl;
        }
        if (a > 1) cout << a << ' ' << 1 << endl;
        cout << endl;
    }
    
}
```







