# Day 1 后端笔试训练题

> 吐槽一下，字节的码上掘金的代码测试平台实在是有点逆天的
>
> 连测试数据都没有...



## 题目 1



> 实现一个 36 进制的加法 0-9 a-z。
>
> 示例
>
> 输入：["abbbb","1"]，输出："abbbc"
>
> 限定语言：C、C++、Java、Python、JavaScript V8、Go

思考：

实现36进制是抖音面试常考的题目，“此题在data数据平台后端一面，教育前端二面均出现过，最常出现在第三轮面试，涉及教育，抖音，data等部门。”

这道题应该还有个隐含的条件，即：不允许把36进制数字整体转为10进制数字，计算出10进制数字的相加结果再转回为36进制，不然会过于简单

不过将每一位数字转换回36进制下代表的真实数字还是可以的



在实现36进制加法前，我们可以先实现一个熟悉的10进制加法：

```cpp
#include <iostream>
#include <string>
using namespace std;

string add10Strings(string num1, string num2) {
    // 每一位的算法都等于num1的这一位 + num2的这一位 + 进位
    // 而且只要这三个里面任意一个还有数就要继续执行
    // 代表这两个数正在进行计算的位数
    int i = num1.size() - 1;
    int j = num2.size() - 1;
    // 代表进位
    int carry = 0;
    // 代表最后输出的字符串
    string res;
    // 不能直接将每一位数相加，因为会出现少位的情况
    while (i >= 0 || j >= 0 || carry) {
        int x = i >= 0 ? num1[i] - '0': 0; // 注意这里string 里面取出来之后要进行字符的相加减，让其自动转化为int类型变量
        int y = j >= 0 ? num2[j] - '0': 0;
        int temp = x + y + carry;
        res += '0' + temp % 10; // 相加之后自动转成字符串，注意这里string等式两边各自至少要有一个字符串
        carry = temp / 10;
        i --; j --;
    }
    reverse(res.begin(), res.end());
    return res;

}

int main () {
    string a, b, c;
    cin >> a >> b;
    c = add10Strings(a, b);
    cout << c << endl;
    return 0;
};
```



关于字符串相加的输出顺序：

```cpp
int main () {
    int a = 1, b = 2;
    string res;
    res += '0' + a + b;
    res += '0' + a;
    res += '0' + b;
    cout << res; // 输出是312
    return 0;
}
```



```cpp

//实现一个 36 进制的加法 0-9 a-z。

#include <iostream>
#include <string>
using namespace std;

int getInt(char ch) {
    if (ch >= '0' && ch <= '9') return ch - '0'; // 注意必须是ch - '0'
    else return (ch - 'a' + 10);
}

char getChar(int n) {
    if (n <= 9) return n + '0';  // 注意必须是n + '0'，从int强制转化成char，int边必须要有字符，而且必须是+号
    else return n - 10 + 'a';
}

string add36Strings(string num1, string num2) {
    int i = num1.size() - 1;
    int j = num2.size() - 1;
    int carry = 0;
    string res;
    int x, y;
    while (i >= 0 || j >= 0 || carry) {
        x = i >= 0 ? getInt(num1[i]) : 0;
        y = j >= 0 ? getInt(num2[j]) : 0;
        int temp = x + y + carry;
        carry = temp / 36;
        res += getChar(temp % 36);
        i--, j--;
    }
    reverse(res.begin(), res.end());
    return res;

}

int main () {
    string a, b;
    cin >> a >> b;
    string c = add36Strings(a, b);
    cout << c << endl;
    return 0;
}
```



关于char和int之间互相转化的知识点：

```cpp
#include <iostream>
using namespace std;

int main () {
    char ch = '8';
    cout << ch << ' ' << ch + '0' << ' ' << ' ' << ch - '0' << endl; // 输出 8 104 8

    int a = ch;
    int b = ch + '0';
    int c = ch - '0';
    cout << a << ' ' << b << ' ' << c << endl; // 输出 56 104 8

    int n = 8;
    cout << (char)(n + '0') << ' ' << (char)(n - '0') << endl << (char)(n) << endl; // 输出 8 乱码 和空

    // 8 的ASCII码值是56
    // char想要转换成原数字的int 需要char - '0'
    // int想要转换成原数字的char 需要int + '0'
    return 0;
}
```





## 题目 2



> 抖音电影票业务支持电影院选座，需要在用户买票时自动推荐座位，如果一个用户买了多张票，则需要推荐相邻(上下相邻、左右相邻都可)的座位。现在使用一个二维数组来表示电影院的座位，数组中 0 表示未被选座，1 表示已被选座或者为障碍物，请实现一个方法求出给定影院中最大可推荐的相邻座位个数。
>
> 示例
>
> 输入：
>
> [1,0,0,1,0,0,0]
>
> [1,0,0,0,0,1,1]
>
> [0,0,0,1,0,0,0]
>
> [1,1,0,1,1,0,0]
>
> 输出：18
>
> 限定语言：C、C++、Java、Python、JavaScript V8、Go



```cpp
```





## **题目3**

> 有效 IP 地址正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。
>
> 例如："0.1.2.201" 和 "192.168.1.1" 是有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是无效 IP 地址。
>
> 给定一个字符串 s，非数字的字符可替换为任意不包含在本字符串的数字，同样的字符只能替换为同样的数字，用以表示一个 IP 地址，返回所有可能的有效 IP 地址，这些地址可以通过在 s 中插入 '.' 来形成。你不能重新排序或删除 s 中的任何数字，你可以按任何顺序返回答案。
>
> **示例 1**
>
> 输入：20212118136
>
> 输出：
>
> 20.212.118.136
>
> 202.12.118.136
>
> 202.121.18.136
>
> 202.121.181.36
>
> **示例 2**
>
> 输入：11a2b22a037
>
> 输出：114.252.240.37
>
> **限定语言：**C、 C++、Java、Python、JavaScript V8、Go



```cpp
```









