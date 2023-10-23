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



