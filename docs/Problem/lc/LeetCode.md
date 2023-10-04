# LeetCode

## About LeetCode

leetcode相比于oj题就和奥赛题对于普通数学题一样，主要需要坚持下来

氛围很重要，每周跟着刷

刷四五百道题面试一般问题不是很大

### 思维

算法要把每一步搞懂，要知道为什么这么做，这个是最重要的，防止遇到新题不会做

先看思路再看代码，而不要对着代码去猜思路



### 写代码

一般写的时间和调试时间一样长

这个调试bug的能力很重要



### 英语

还是需要锻炼一下自己英语看题和英语说思路的能力的



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
> 2. 注意hash[nums[i]] = i;的使用



### [2. Add Two Numbers](https://leetcode.cn/problems/add-two-numbers/)



