# 代码随想录笔记

## 1. 二分查找

二分查找的数学理解是单调函数的有解问题

注意点：

1. 在C++中STL的容器和算法中用的都是左闭右开区间，所以尽量使用左闭右开的区间来写二分查找

2. 在刷题时思考如果最后区间只剩下一个数或者两个数，自己的写 法是否会陷入死循环，如果某种写法无法跳出死循环，则考虑尝试另一种写法。



### [844. 比较含退格的字符串](https://leetcode.cn/problems/backspace-string-compare/)

```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        return get(s) == get(t);
    }
    string get(string& s) {
        string res;
        for (auto c : s) {
            if (c == '#') {
                if (res.size()) res.pop_back();
            }
            else res+= c;
        }
        return res;
    }
};
```

#### O1空间复杂度：

```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        changestring(s);
        changestring(t);
        return s==t;
    }
    void changestring(string &s)
    {
        int slow=0;
        for(int fast=0;fast<s.size();fast++)
        {
            if(s[fast]!='#')
            s[slow++]=s[fast];
            else if(slow!=0)
                slow--;
        }
        s.resize(slow);
    }
};

```

### [977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        // 不要忘记定义vector<int>的时候进行定义数组大小
        vector<int> res(nums.size(), 0);
        int l = 0, r = nums.size() -1, i = nums.size() -1 ;
        while (l <= r && i >= 0) {
            if (nums[l] + nums[r] <= 0) {
                res[i--] = nums[l] * nums[l];
                l++;
            } else {
                res[i--] = nums[r] * nums[r];
                r--;
            }
        }
        return res;
    }
};
```



### [209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int i = 0, j = 0, ans = INT_MAX, res = 0;
        while (j < nums.size()) {
            res += nums[j];
            while (res >= target) {
                ans = min(ans, j - i + 1);
                res -= nums[i];
                i++;
            }
            j++;
        }
        return (ans == INT_MAX) ? 0 : ans;
    }
};
```

