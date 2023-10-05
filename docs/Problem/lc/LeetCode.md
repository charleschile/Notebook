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



## 10.4

### [10. Regular Expression Matching](https://leetcode.cn/problems/regular-expression-matching/)



## 10.5

