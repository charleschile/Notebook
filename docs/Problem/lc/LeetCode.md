# LeetCode

## About LeetCode

leetcode相比于oj题就和奥赛题对于普通数学题一样，主要需要坚持下来

氛围很重要，每周跟着刷

刷四五百道题面试一般问题不是很大

### 思维

算法要把每一步搞懂，要知道为什么这么做，这个是最重要的，防止遇到新题不会做

先看思路再看代码，而不要对着代码去猜思路

555555

### 写代码

一般写的时间和调试时间一样长

这个调试bug的能力很重要



### 英语

还是需要锻炼一下自己英语看题和英语说思路的能力的

### debug

#### 1. 需要使用long long类型存储

int 4个字节 -2147483648 到 2147483647

long long 8 个字节 -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807

```bash
Line 8: Char 22: runtime error: signed integer overflow: 10 * 964632435 cannot be represented in type 'int' (solution.cpp)
```





### 技巧和需要知道的知识

#### 知识：关于二维布尔值的定义

使用如下语句创建bool二维数组的时候,初始化的值是false

```cpp
vector<vector<bool>> f(n + 1, vector<bool>(m + 1));
```

创建了一个二维的布尔型（bool）向量（vector）数组 `f`，其大小为 `(n+1)` 行，每行有 `(m+1)` 列。

`vector` 是C++标准库中的动态数组容器，`vector<bool>` 表示存储布尔类型的动态数组

`vector<vector<bool>>`：这表示一个二维的动态数组。外部的 `vector` 包含内部的 `vector<bool>`。这是一个向量的向量，其中外部 `vector` 的每个元素都是一个内部 `vector<bool>`。这样就创建了一个二维布尔数组或矩阵，其中外部 `vector` 表示行，内部 `vector<bool>` 表示每一行中的列。



外部的 `f(n + 1, ...)` 部分用于定义 `f` 的行数，它创建了一个 `vector<vector<bool>>`，其中有 `n + 1` 行。这是一个外部向量，每个元素都是一个内部的向量。

内部的 `vector<bool>(m + 1)` 部分用于定义 `f` 中每行的列数，它创建了一个内部 `vector<bool>`，其中有 `m + 1` 个布尔元素。这是内部向量，用于表示每一行中的列。



那么创建一个三位的布尔数组:

```cpp
	// 创建一个三维布尔型向量数组
    // 初始化为false，可以根据需要初始化为true
    vector<vector<vector<bool>>> threeDArray(n, vector<vector<bool>>(m, vector<bool>(k, false) ));
	threeDArray[0][1][2] = true;
```



#### 知识: 正则表达式

1. **字符匹配**：正则表达式用于匹配具体的字符。例如，`a` 匹配字符 "a"，`123` 匹配字符串 "123"。
2. **通配符**：`.` 表示匹配任意字符，除了换行符。例如，`a.b` 匹配 "axb"、"aab"、"a1b" 等。
3. **字符类**：用方括号 `[]` 来定义一个字符类，可以匹配括号内的任何一个字符。例如，`[abc]` 匹配 "a"、"b" 或 "c" 中的任何一个字符。
4. **字符范围**：在字符类中可以使用连字符 `-` 来表示一个字符范围。例如，`[a-z]` 匹配任何小写字母。
5. **重复**：使用 `{}`、`*`、`+`、`?` 等来表示字符或子表达式的重复次数。例如，`a{3}` 匹配 "aaa"，`a*` 匹配零次或多次的 "a"。
6. **起始和结束**：`^` 表示字符串的开始，`$` 表示字符串的结束。例如，`^abc` 匹配以 "abc" 开头的字符串。
7. **或操作**：使用 `|` 来表示或操作，匹配多个可能的模式中的一个。例如，`cat|dog` 匹配 "cat" 或 "dog"。
8. **分组**：使用 `()` 来创建一个子表达式，可以对子表达式进行重复、或操作等操作。例如，`(ab)+` 匹配 "ab"、"abab"、"ababab" 等。

需要注意的是`.*`可以用来匹配任意的字符串,原因是`*`代表的是重复任意个数的`.`,也就是这两个符号可以匹配任意数量的任意字符串



#### 知识: 逻辑预算符的优先级

在c++中的&&优先级高于||

#### 知识：数组的大小

只有标准容器才可以使用`size()`

而用`string reps[]`定义的数组的大小需要使用sizeof()，不过由于reps[1]是字符串所以可以使用reps[1].size()



#### 知识：字符串的处理

string下字符串的相等可以直接使用等号：

```cpp
#include <vector>
#include <string>
#include <iostream>
using namespace std;
int main() {
    string s = "adfs;jlk";
    string pattern = "d";
    if (s.substr(1, 1) == pattern) cout << "yes" << endl; // 输出yes
    return 0;
}

```

注意substr()的使用！！！



#### 知识：pair键值对的使用

##### pair键值对定义

```cpp
pair<int, int> res(INT_MAX, INT_MAX);
```

这里两个初始的值都被设成了INT_MAX

##### 键值对的比较

键值对的比较是逐个元素的比较，就是先比较第一个，如果相同再比较第二个

```cpp
pair<int, int> res(INT_MAX, INT_MAX);
res = min(res, make_pair(abs(s-target), s));
```

##### 键值对第二个元素的返回

```cpp
return res.second;
```



##### 键值对数组的定义

注意这里`const auto&`

- `const` 表示 `kvp` 是只读的，你不能在循环中修改容器中的元素。
- `auto&` 声明了一个引用，因此 `kvp` 会指向容器中的实际元素，这意味着在循环中使用 `kvp` 时，你实际上是在操作容器中的元素，任何修改都会反映到容器本身。

```cpp
	vector<pair<string, int>> keyValuePairs;

    keyValuePairs.push_back({"orange", 1});

    keyValuePairs.push_back(make_pair("apple", 5));

    // 访问键值对
    for (const auto& kvp : keyValuePairs) {
        cout << "The value of " << kvp.first << " is: " << kvp.second << endl;
    }
```



##### 哈希表的定义(unordered_map)

`std::unordered_map` 是一个哈希表数据结构，它用于存储键-值对，其中键是唯一的，而值可以重复。

`hash.count(k)` 是用于检查哈希表中是否存在特定键 `k` 的成员函数，它返回一个整数值，表示指定键 `k` 在哈希表中的出现次数。

```cpp
unordered_map<int, int> hash;
hash.count(k)
```



#### 知识：leetcode中链表结构体的定义

```cpp
 struct ListNode {
      int val;
      ListNode *next;
      ListNode() : val(0), next(nullptr) {}
      ListNode(int x) : val(x), next(nullptr) {}
      ListNode(int x, ListNode *next) : val(x), next(next) {}
  };
```



#### 知识：栈的使用

```cpp
//栈的定义
stack<char> stk;

stack, 栈
    size()
    empty()
    push()  向栈顶插入一个元素
    top()  返回栈顶元素
    pop()  弹出栈顶元素

```



#### 题型：括号序列问题

| 123  |  {   |
| :--: | :--: |
| 125  |  }   |
|  91  |  [   |
|  93  |  ]   |
|  40  |  (   |
|  41  |  )   |

可以发现每组括号的ASCII码表之差<2，可以用来判断每组括号是否闭合

即`abs(c -stk.top()) < 2`

同时，只有一种括号的括号序列合法的话，需要满足：

1. 任意前缀中左括号的数量大于等于右括号的数量
2. 总字符串中左右括号的数量相等





## 10.1

### [1. Two Sum](https://leetcode.cn/problems/two-sum/)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        for (int i = 0; i < nums.size(); i++) {
            int k = target - nums[i];
            if (hash.count(k)) {
                return {hash[k], i};
                break;
            }
            hash[nums[i]] = i;
        }
        return {};
    }
};
```

> 1. 注意hash.count()的使用
> 3. 注意hash[nums[i]] = i;的使用



### [2. Add Two Numbers](https://leetcode.cn/problems/add-two-numbers/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        // 凡是需要特判第一个点的地方，都可以加入一个虚拟头节点
        ListNode* dummy = new ListNode(-1);
        ListNode* cur = dummy;
        int carry = 0;
        while (l1 || l2 || carry) {
            if (l1) carry += l1->val, l1 = l1->next;
            if (l2) carry += l2-> val, l2 = l2->next;
            cur = cur->next = new ListNode(carry % 10);
            carry /= 10;
        }
        return dummy->next;

    }
};
```



### [3. Longest Substring Without Repeating Characters](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

这类问题考虑的是怎么将所有的情况考虑到



```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<int, int> hash;
        int res = 0;
        for (int i = 0, j = 0; j < s.size(); j++) {
            hash[s[j]]++;
            while (hash[s[j]] > 1) hash[s[i++]] --;
            res = max(res, j - i + 1);
        }
        return res; 
    }

};
```



## 10.2

### [4. Median of Two Sorted Arrays](https://leetcode.cn/problems/median-of-two-sorted-arrays/)

vector数组中size函数的返回值是size_type ，而 size_type 的类型是：unsigned int，min接受int型参数，所以需要强转

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int t = nums1.size() + nums2.size();
        if (t % 2 == 0) {
            int left = find(nums1, 0, nums2, 0, t / 2); // find找的是第t/2小的数
            int right = find (nums1, 0, nums2, 0, t / 2 + 1);
            return (left + right) / 2.0;
        } else return find(nums1, 0, nums2, 0, t / 2 + 1);
    }


    int find(vector<int>& nums1, int i, vector<int>& nums2, int j, int k) {
        // 首先要防止越界的情况发生，那么就要把剩下的较长的数组存储再nums2
        if (nums1.size() - i > nums2.size() - j) return find(nums2, j, nums1, i, k);
        if (nums1.size() == i) return nums2[j + k - 1];
        if (k == 1) return min(nums1[i], nums2[j]);
        
        // 递归逻辑
        // 比较每个sub数组中第k/2个的数的大小，注意nums的长度比较短
        // 而且我们也不能确定k是奇数还是偶数，所以对于另一个数组加上（k - k/2）才行
        // vector数组中size函数的返回值是size_type ，而 size_type 的类型是：unsigned int，min接受int型参数，所以需要强转
        int si = min((int)nums1.size(), (i + k / 2));
        int sj = j + k - k /2;
        // 这里指的是第几个，所以必须要 -1
        if (nums1[si - 1] > nums2[sj  - 1]) {
            return find(nums1, i, nums2, sj, k - (sj - j));
        } else return find(nums1, si, nums2, j, k - (si - i));
    } 
};
```





### [5. Longest Palindromic Substring](https://leetcode.cn/problems/longest-palindromic-substring/)

palindromic substring 回文字符串

遇到问题先用暴力解法试试

```cpp
class Solution {
public:
    string longestPalindrome(string s) {

        string res;
        for (int i = 0; i < s.size(); i++) {
            // 回文字符串为奇数的情况
            // 使用双指针
            int m = i - 1, n = i + 1;
            while (m >= 0 && n <s.size() && s[m] == s[n]) {
                m--, n++;
            }
            if (n - m - 1 > res.size()) res = s.substr(m + 1, n - m - 1);

            // 回文字符串为偶数的情况
            m = i, n = i + 1;
            while (m >= 0 && n < s.size() && s[m] == s[n]) {
                m--, n++;
            }
            if (n - m - 1> res.size()) res = s.substr(m + 1, n - m - 1);
        }

        return res;
    }

};
```



### [6. Zigzag Conversion](https://leetcode.cn/problems/zigzag-conversion/)

zigzag pattern 之字形

legibility 辨识性

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        string res;
        if (numRows == 1) return s;
        for (int i = 1; i <= numRows; i ++) {
            if (i == 1 || i == numRows) {
                for (int j = i - 1; j < s.size(); j =j + (2 * numRows - 2)) {
                    res += s[j];
                }
            } else {
                for (int l = i - 1, r = i - 1 + 2*(numRows - i); l < s.size() || r < s.size(); l += 2 * numRows - 2, r += 2 * numRows - 2) {
                    if (l < s.size()) res += s[l];
                    if (r < s.size()) res += s[r];
                }
            }
        }

        return res;
    }
};
```







## 10.3

### [7. Reverse Integer](https://leetcode.cn/problems/reverse-integer/)

```cpp
class Solution {
public:
    int reverse(int x) {
        // 按照题意，res要被定义成int类型的变量
        int res = 0;
        while (x) {
            // 注意看题意超出32位整数需要return0！
            // C++里面负数模上10是负数，这个性质可以使写代码变得简单
            if (res > 0 && res > (INT_MAX - x % 10) /10) return 0;
            if (res < 0 && res < (INT_MIN - x % 10) /10) return 0;
            res = 10 * res + x % 10;
            x /= 10;
        }

        return res;

    }
};
```

### [8. String to Integer (atoi)](https://leetcode.cn/problems/string-to-integer-atoi/)

clamp 截断

```cpp
class Solution {
public:
    int myAtoi(string s) {
        char f;
        int res = 0;
        int i = 0;

        while (s[i] == ' ') i++;
        if (s[i] == '-' || s[i] == '+') {
            f = s[i];
            i++;
        }
            
        while (i < s.size() && s[i] >= '0' && s[i] <= '9') {
            if (res > (INT_MAX - (s[i] - '0')) / 10 && f == '-') return INT_MIN;
            // 无论是前面没有符号或者有+的，都是正数
            if (res > (INT_MAX - (s[i] - '0')) / 10) return INT_MAX;
            res = 10 * res + (s[i] - '0');
            i ++;
        }
        
        // cout << "f = " << f <<endl;
        if (f == '-') return -res;
        else return res;
    }
};
```



### [9. Palindrome Number](https://leetcode.cn/problems/palindrome-number/)

palindrome 回文

#### 1. 转换成字符串处理双指针（最慢的做法）

```cpp
class Solution {
public:
    bool isPalindrome(int x) {

        string s = to_string(x);
        for (int i = 0, j = s.size() - 1; i < s.size() && j >= 0; i++, j--) {
            if (i == j) return true;
            if (s[i] != s[j]) {
                return false;
                break;
            }
        }
        return true;
    }
};
```



#### 2. 反转字符串进行比较

注意rbegin()和rend()

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        string s = to_string(x);
        return s == string(s.rbegin(), s.rend());
        return true;
    }
};
```

#### 3. 使用整数反转，倒序一位一位*10 + 1，然后进行比较

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        // 初始化的时候一定要给一个值！！！
        long long res = 0;
        int y = x;
        if (x < 0) return false;
        while (x) {
            res = res * 10 + x % 10;
            x /= 10;
        }
        return res == y;
    }
};
```



## 10.22

### [10. Regular Expression Matching](https://leetcode.cn/problems/regular-expression-matching/)

怎么看出来是的dp的：给两个字符串求最长公共子序列，给两个字符串让我们求边际距离，给两个字符串问会不会匹配（来自经验）



通用的分析过程，降低分析难度

从集合角度来看问题

时间复杂度是n^2

要么循环要么递归，递归更容易理解，但是时间会长一些



一看是一个序列模型



状态表示（靠经验）：两个序列一般使用两维来表示，



集合f(i, j) 在所有方式里面是否存在一个合法的方案,表示的集合是所有s[1-i]和[1-j]的匹配方案

属性:bool是否存在一个合法方案

正常来说就需要暴力搜索了



状态计算：

1. 如果p[j]不是x*(要把`*`和它前面的那个字符看成一个整体),那么直接匹配就可以了s[i]==p[j]  ||  p[j]=='.' && f(i - 1, j - 1) (详细的来讲就是,最后比较的那两个字符相等,或者p的最后一位是通配符,并且这两个最后字符之前的序列都是匹配的)

2. 如果p[j]是x*,那么就要开始考虑`x*`代表的是多少个字符,千万注意是把`*`和他前面的那个字符看成一个整体!

如果这个整体代表0个字符那么就需要f(i, j - 2)

如果代表1个字符:f(i - 1, j - 2) && si和pj也要匹配

如果代表2个字符:f(i - 2, j - 2) && si && si -1

所以:

f(i, j) = f(i , j- 2) || f(i - 1, j - 2) & si || f(i -2, j - 2) & si & si -1

f(i - 1, j) = f(i - 1, j -2) || f(i -2, j -2) & si-1...



所以f(i, j) =f(i, j - 2) ||  f(i - 1, j) &si与p[j]匹配



leetcode的测试样例经过加强之后已经不用考虑略过p[j + 1]是*的这种情况了,原因是会出现`a***b`



```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.size(), m = p.size();
        // 需要建立二维布尔数组来存储到现在为止，所有s中的字符是否已经被p中的字符匹配
        s = ' ' + s, p = ' ' + p;
        vector<vector<bool>> f(n + 1, vector<bool>(m + 1));
        // 不要忘记给初始的赋值
        f[0][0] = true;
        // 因为是循环，那么p中的字符数量很有可能会超过s中现在循环到的字符数量
        for (int i = 0; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (i && p[j] != '*') {
                    f[i][j] = f[i - 1][j - 1] && (s[i] == p[j] || p[j] == '.');
                } else if (p[j] == '*') {
                    f[i][j] = f[i][j - 2] || i && f[i - 1][j] && (s[i] == p[j - 1] || p[j - 1] == '.');
                }
            }
        }
        return f[n][m];
    }
};
```



###  [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        // 暴力做法超出时间限制了
        // 那么有两条边的问题就可以用双指针进行优化
        // 只有移动短边才有可能使水面上升
        // 木桶容量由短板决定, 移动长板的话, 水面高度不可能再上升, 而宽度变小了, 所以只有通过移动短板, 才有可能使水位上升.
        int res = 0;
        for (int i = 0, j = height.size() - 1; i < j;) {
            res = max(res, (j - i) * min(height[i], height[j]));
            if (height[j] < height[i]) j--;
            else i++;
        }
        return res;
    }
};
```



### [12. 整数转罗马数字](https://leetcode.cn/problems/integer-to-roman/)

```cpp
class Solution {
public:
    string intToRoman(int num) {
        string res;
        int values[] = {
            1000,
            900, 500, 400, 100,
            90, 50, 40, 10,
            9, 5, 4, 1
        };
        string reps[] = {
            "M",
            "CM", "D", "CD", "C",
            "XC", "L", "XL", "X",
            "IX", "V", "IV", "I"
        };
        for (int i = 0; i < 13; i++) {
            while (num >= values[i]) {
                num -= values[i];
                res += reps[i];
            }
        }
        return res;
    }
};
```



## 10.23

### [13. 罗马数字转整数](https://leetcode.cn/problems/roman-to-integer/)

> 一道纯粹的string 语法题，用到了substr()和empty()
>
> 也可以使用哈希表来做，语法上更加漂亮

```cpp
class Solution {
public:
    int romanToInt(string s) {
        int res = 0;
        int value[] = {
            1000,
            900, 500, 400, 100,
            90, 50, 40, 10,
            9, 5, 4, 1
        };
        string reps[] = {
            "M",
            "CM", "D", "CD", "C",
            "XC", "L", "XL", "X",
            "IX", "V", "IV", "I"
        };
        for (int i = 0; i < 13 && !s.empty(); i++) {
            while (!s.empty() && s.substr(0, reps[i].size()) == reps[i]) {
                res += value[i];
                s = s.substr(reps[i].size(), s.size() - reps[i].size());
            }
        }
        return res;
    }
};
```





```cpp
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> hash;
        hash['I'] = 1, hash['V'] = 5;
        hash['X'] = 10, hash['L'] = 50;
        hash['C'] = 100, hash['D'] = 500;
        hash['M'] = 1000;
        int res = 0;
        for (int i = 0; i < s.size(); i++) {
            if (i < s.size() - 1 && hash[s[i]] < hash[s[i + 1]]) {
                res -= hash[s[i]];
            } else res += hash[s[i]];
        }
        return res;
    }
};
```



### [14. 最长公共前缀](https://leetcode.cn/problems/longest-common-prefix/)

前缀的意思是下标连续，不然就变成dp问题了

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string res = "";
        for (int i = 0; i < strs[0].size(); i++) {
            char pattern = strs[0][i];
            for (int j = 0; j < strs.size(); j++) {
                if (i < strs[j].size() && strs[j][i] == pattern) continue;
                else return res;
            }
            res += pattern;
        }
        return res;
    }
};
```





### [15. 三数之和](https://leetcode.cn/problems/3sum/)

双指针做法一定要有序

> 这道题目最重要的一点就是将n^3的时间复杂度降下来
>
> 在i固定的情况下，并且保证j<k，如果我们找到了第一组=0的三个数
>
> 那么枚举j变大时，k只能变小
>
> 这样我们就做到了在i不变的情况下，j和k一共最多只枚举n个数而不是n^2





```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 2; i++) {
            if (i && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1, k = nums.size() - 1; j < k; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                while (j < k - 1 && nums[i] + nums[j] + nums[k - 1] >= 0) k--;
                if (nums[i] + nums[j] + nums[k] == 0) res.push_back({nums[i], nums[j], nums[k]});  
            }
        }
        return res;

    }
};
```



## 10.24

### [16. 最接近的三数之和](https://leetcode.cn/problems/3sum-closest/)

- 键值对pair的应用,`make_pair`以及`return res.second`
- 找到了>= target的最小值，那么这个数的前一位必定是<target的最大值

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        pair<int, int> res(INT_MAX, INT_MAX);
        for (int i = 0; i < nums.size() - 2; i++) {
            for (int j = i + 1, k = nums.size() - 1; j < k; j++) {
                while (j < k - 1 && nums[i] + nums[j] + nums[k - 1] >= target) k--;
                int sum = nums[i] + nums[j] + nums[k];
                res = min(res, make_pair(abs(sum - target), sum));
                if (k - 1 > j) {
                    sum = nums[i] + nums[j] + nums[k - 1];
                    res = min(res, make_pair(abs(target - sum), sum));
                }
            }
        }
        return res.second;
    }
};
```



### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

- 注意到dfs的形式
- 使用digits.empty()
- auto c : strs[digits[u] - '0']

```cpp
class Solution {
public:
    vector<string> ans;
    string strs[10] = {
        "", "", "abc", "def",
        "ghi", "jkl", "mno",
        "pqrs", "tuv", "wxyz"
    };
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return ans;
        dfs(digits, 0, "");
        return ans;
    }
    void dfs(string& digits, int u, string path) {
        if (u == digits.size()) ans.push_back(path);
        else {
            for (auto c : strs[digits[u] - '0']) {
                dfs(digits, u + 1, path + c);
            }
        }
    }
};
```





### [18. 四数之和](https://leetcode.cn/problems/4sum/)

10.27做题心得：

1. 如果出现溢出的情况，先特判一下输入  if (nums.size() < 4) return ans;
1. 注意看输入的大小，注意开long long 

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ans;
        if (nums.size() < 4) return ans;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 3; i++) {
            if (i && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < nums.size() -2; j++) {
                if (j >= i + 2 && nums[j] == nums[j -1]) continue;
                for (int m = j + 1, n = nums.size() - 1; m < n; m++) {
                    if (m >= j + 2 && m < n && nums[m] == nums[m - 1]) continue;
                    while((long long) nums[i] + nums[j] + nums[m] + nums[n - 1] >= target && m < n- 1) n--;
                    if ((long long)nums[i] + nums[j] + nums[m] + nums[n] == target) ans.push_back({nums[i], nums[j], nums[m], nums[n]});
                }
            }
        }
        return ans;
    }
};
```





## 10.25

### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // 在所有有可能会删除头节点的链表题目中，需要添加虚拟头节点
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        // 先遍历一遍整个链表，k记录的是包含虚拟头节点dummy的总链表的长度
        int k = 0;
        for (auto ptr = dummy; ptr; ptr = ptr->next) k++;
        
        auto ptr = dummy;
        for (int i = 0; i < k - n - 1; i++) ptr = ptr->next;
        
        ptr->next = ptr->next->next;
        return dummy->next;
    }
};
```







### [20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)



```cpp
class Solution {
public:
    bool isValid(string s) {
        // 先进后出的数据结构是stack
        stack<char> stk;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[') {
                stk.push(c);
            } else {
                if (stk.size() && abs(c - stk.top()) <= 2) stk.pop();
                else return false;
            }
        }
        return stk.empty();
    }
};
```



### [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        auto dummy = new ListNode(-1), tail = dummy;
        while (list1 && list2) {
            if (list1->val <= list2->val) {
                tail = tail->next = list1;
                list1 = list1->next;
            } else {
                tail = tail->next = list2;
                list2 = list2->next;
            }
        }
        if (list1 == NULL) tail->next = list2;
        else tail->next = list1;
        return dummy->next;
    }
};
```





## 10.26

### [22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)

```cpp
class Solution {
public:
    vector<string> res;
    vector<string> generateParenthesis(int n) {
        dfs(n, 0, 0, "");
        return res;
    }
    void dfs (int n, int l, int r, string seq) {
        if (l == n && r == n) res.push_back(seq);
        else {
            if (l < n) dfs(n, l + 1, r, seq + '(');
            if (r < n && l > r) dfs(n, l, r + 1, seq + ')');
        }
    }
};
```



### [23. 合并 K 个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

使用堆来维护第k个指针

用堆将时间复杂度从优化成nlogk

优先队列就是堆

优先队列自定义比较函数

优先队列是大根堆，所以会把大的放在前面



```cpp
std::priority_queue<T, Container, Compare>
```

`Compare`：这是一个比较函数或者函数对象，用于定义元素之间的优先级比较规则。`std::greater<int>` 是一个标准库提供的函数对象，它用于创建一个最小堆。





#### 关于比较规则的实现

> 优先队列cmp和sort的效果是相反

所有STL容器和库函数默认使用的是小于号，如果加上greater<>参数，那么会默认使用大于号。在上面的代码中优先队列会默认用一对小括号表示小于号，并且默认会构造一个大根堆，所以我们把小括号里的关系变一下，最后就可以得到小根堆了。

一下是C++中，`std::greater<int>`的具体实现：

```cpp
template <class T>
struct greater {
    bool operator() (const T& x, const T& y) const {
        return x > y;
    }
};

```

重载()的原因是`operator()` 的重载使对象可以像函数一样被调用，因为它是函数调用运算符。这使得函数对象可以灵活地封装操作，可以在其中包含状态，实现自定义的行为，并且可以用于泛型编程。

比如：

```cpp
#include <iostream>

struct MyComparator {
    bool operator()(int a, int b) const {
        return a > b;
    }
};

int main() {
    MyComparator cmp;
    bool result = cmp(5, 3); // 使用函数对象调用，比较5和3
    std::cout << result << std::endl; // 输出1，因为5 > 3
    return 0;
}

```





#### 优先队列合并代码：时间 O(kn * logk), 空间 O(k)

注意：`auto dummy = new ListNode(-1), tail = dummy;(return dummy->next)`的实现还能是` ListNode dummy, *cur = &dummy;(return dummy.next)`

可以不把 head 设为 ListNode * 指针类型, 而是把 head 设为 ListNode 类型，这样 就不用 考虑 内存的问题了。不把 head作为指针 new出来 确实会 节省内存，内存消耗 由 22.1MB 变为 12.7MB。

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    struct Cmp {
        bool operator() (ListNode* a, ListNode* b) {
            return a->val > b->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, Cmp> heap;
        auto dummy = new ListNode(-1), tail = dummy;
        for (auto l : lists) if (l) heap.push(l);

        while (heap.size()) {
            auto t = heap.top();
            heap.pop();
            tail->next = t;
            tail = tail->next;
            if (t->next) heap.push(t->next);
        }
        return dummy->next;
    }

};
```



#### 分治合并代码： O(kn * logk), 递归栈空间 O(logk)

`cur->next = a ? a : b;`

- 如果 `a` 非空（即 `a` 还有剩余节点），那么将 `cur->next` 指向 `a`，并将 `a` 向后移动一个节点，同时 `cur` 也向后移动一个节点。
- 如果 `a` 为空，那么将 `cur->next` 指向 `b`，并将 `b` 向后移动一个节点，同时 `cur` 也向后移动一个节点。

##### 回忆归并排序算法模板题

```cpp
#include <iostream>
using namespace std;
const int N = 1e5+10;
int q[N], tmp[N];

void merge_sort (int q[], int l, int r) {
    if (l >= r) return;
    int mid = l + r >> 1;
    merge_sort(q, l, mid);
    merge_sort(q, mid + 1, r);
    int i = 0, j = l, k = mid + 1;
    while (j <= mid && k <= r) {
        if (q[j] <= q[r]) tmp[i++] = q[j++];
        else tmp[i++] = q[k++];
    }
    while (j <= mid) tmp[i++] = q[j++];
    while (k <= r) tmp[i++] = q[k++];
    for (int i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
} 

int main () {
    int n;
    
    cin >> n;
    for (int i = 0; i < n; i++) cin >> q[i];
    merge_sort(q, 0, n - 1);
    for (int i = 0; i < n; i++) cout << q[i] << " " << endl;
    return 0;
}
```





注意由于返回的仍然是原来链表的头节点地址，所以不会造成悬空指针

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode * a, ListNode * b) {
        ListNode dummy, *cur = &dummy;
        while (a && b) {
            if (a->val < b->val) cur = cur->next = a, a = a->next;
            else cur = cur->next = b, b = b->next;
        }
        cur->next = a ? a : b;
        return dummy.next;
    }
    ListNode* merge(vector<ListNode*>& lists, int l, int r) {
        if (l == r) return lists[l];
        if (l > r) return nullptr;
        int mid = (l + r) >> 1;
        return mergeTwoLists(merge(lists, l, mid), merge(lists, mid + 1, r));
        
    }
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int n = lists.size();
        if (!n) return nullptr;
        return merge(lists, 0, n - 1);
    }
};
```





### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

不用害怕多建几个指针没有关系

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* cur = dummy;
        while (cur->next && cur->next->next) {
            ListNode* p1 = cur->next;
            ListNode* p2 = cur->next->next;
            p1->next = p2->next;
            cur->next = p2;
            p2->next =  p1;
            cur = p1;
        }
        return dummy->next;
    }
};
```



### [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode * dummy = new ListNode(-1);
        dummy->next = head;
        for (auto p = dummy;;) {
            auto q = p;
            for (int i = 0; i < k && q; i++) q = q->next;
            if (!q) break;
            auto a = p->next, b = a->next;
            for (int i = 0; i < k - 1; i++) {
                auto c = b->next;
                b->next = a;
                a = b, b = c;
            }
            auto c = p->next;
            p->next = a;
            c->next = b;
            p = c; // 注意是每k个节点一组进行翻转
        }
        return dummy->next;
    }
};
```



### [26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)

注意题目中指出了数组中结尾的数并不重要！

所以直接将后面符合要求的数字填在前面就可以了！！！

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        // 第一个指针遍历所有的数
        // 第二个指针存下所有第一次出现的数
        int j = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (i == 0 || (nums[i] != nums[i - 1])){
                nums[j++] = nums[i];
            }
        }
        return j;
    }
};
```



### [27. 移除元素](https://leetcode.cn/problems/remove-element/)

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int j = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != val) {
                nums[j++] = nums[i];
            }
        }
        return j;
    }
};
```





### [28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/)

#### 纯暴力做法（用来理解思路的练手，正式做题请使用KMP）

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        // 纯暴力两重做法
        for (int i = 0; i < haystack.size(); i++) {
            bool flag = true;
            for (int j = 0; j < needle.size(); j++) {
                if (haystack[i + j] != needle[j]) {
                    flag = false;
                    break;
                }
            }
            if (flag == true) return i;
        } 
        return -1;
    }
};
```



建议画图！

注意kmp算法一点要从1开始比较轻松！！

ne[i]表示的是所有以1为首的前缀和以i结尾的后缀中相同的长度的 最大值

#### KMP做法

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.size(), m = needle.size();
        haystack = ' ' + haystack, needle = ' ' + needle;
        vector<int> ne(m + 1);
        for (int i = 2, j = 0; i <= m; i++) {
            while (j && needle[i] != needle[j + 1]) j = ne[j];
            if (needle[i] == needle[j + 1]) j++;
            ne[i] = j; 
        }
        for (int i = 1, j = 0; i <= n; i++) {
            while (j && haystack[i] != needle[j + 1]) j = ne[j];
            if (haystack[i] == needle[j + 1]) j++;
            if (j == m) return i - m;
        }
        return -1;
    }
};
```







#### 二进制倍增、快速幂的思想！！！

2的n次幂

一定要加long long ，原因是如果是-2^31 取绝对值的话会超过正Int的最大值

```cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        typedef long long LL;
        LL res = 0;
        vector<LL> exp;
        bool is_minus = false;
        if (dividend < 0 && divisor > 0 || dividend > 0 && divisor < 0) is_minus = true;
        LL a = abs((LL)dividend), b = abs((LL)divisor);

        for (LL i = b; i <= a; i = i + i){
            exp.push_back(i);
        }

        for (int i = exp.size() - 1; i >= 0; i--) {
            if (a >= exp[i]) {
                a -= exp[i];
                res += 1ll << i;
                // cout << "a = " << a << "res = " << res << endl;
            }
        }
        if (is_minus) res = -res;
        if (res > INT_MAX) res = INT_MAX;

        return res;
    }
};
```



















what's the problem with my MIPS assembly? 

The problem is : assume that (i) find is a leaf procedure and (ii) no $s registers, the return address register, etc. need to be saved to the stack. 

Note that the array index is returned. Translate the array-based version into MIPS assembly. 

Pointer-based version:

```
int find (int * a, int n, int x) {
    int *p;
    for (p = a + n; p!= a; p--) {
        if (*p == x) return p-a;
    }
    return -1;
}
```



my mips assembly is :

\# a -> $a0, n -> $a1, x -> $a2

addi $sp, $sp, -4

sw $fp, 0($sp)

add $fp, $0, $sp

addi $t0, $0, 4

mul $a1, $t0, $a1

add $t1, $a0, $a1

loop: 

​    beq $t1, $a0, no_found

lw $t2, 0($t1)

beq $t0, $a2, found

addi $t1, $t1, -4

j loop

no_found:

​    li $v0, -1

j exit

found:

​    sub $v0, $t1, $a0

​    div $v0, $v0, $t0

​    j exit

exit:

  lw $fp, 0($sp)

addi $sp, $sp, 4

jr $ra
