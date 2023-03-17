# 一些小技巧

### tips

1. 输出一个整数的各位，直接`char str[n]`，然后输出即可，当成int处理反而麻烦

### C++ 中各种取整

```cpp
// 引入头文件
#include <cmath>
#incldue <math.h>
floor() // 不大于自变量的最大整数
ceil() // 不小于自变量的最大整数
round() // 四舍五入
fix() // 向0取整
```



向上取整技巧：

``` cpp
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

