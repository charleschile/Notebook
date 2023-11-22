# LeetCode 周赛

## 关于debug

### overflow碰到的可能问题

1. 在需要递减的循环里没有选择递减比如` for (int i = nums.size() - 2; i >= 0; i--) `要注意这里的i需要`i--`





### [2240. 买钢笔和铅笔的方案数](https://leetcode.cn/problems/number-of-ways-to-buy-pens-and-pencils/)

```cpp
class Solution {
public:
    long long waysToBuyPensPencils(int total, int cost1, int cost2) {
        // 观察到如果cost1变大，那么循环次数就会变小，那么时间复杂度就会降低
        if (cost1 < cost2) return waysToBuyPensPencils(total, cost2, cost1);
        long long res = 0;
        for (int i = 0; i <= total / cost1; i++) {
            res += (total - cost1 * i) / cost2 + 1;
        }
        return res;
    }
};
```



## 1400-1600



### 2. [2909. 元素和最小的山形三元组 II](https://leetcode.cn/problems/minimum-sum-of-mountain-triplets-ii/)

经典的前后缀分解问题

观察这道题要求的是，中间的数要大于两边，那么就相当于最关键的是中间这个数，所以枚举这个数即可

前缀英文prefix 后缀英文suffix

```cpp
class Solution {
public:
    int minimumSum(vector<int>& nums) {
        int res = INT_MAX;
        vector<int> suf(nums.size());
        suf[nums.size() - 1] = nums[nums.size() - 1];
        for (int i = nums.size() - 2; i >= 0; i--) {
            suf[i] = min(suf[i + 1], nums[i]);
        }

        vector<int> pre(nums.size());
        pre[0] = nums[0];
        for (int i = 1; i < nums.size() - 1; i++) {
            pre[i] = min(pre[i - 1], nums[i]);
            if (nums[i] > pre[i - 1] && nums[i] > suf[i + 1]) {
                res = min(res, nums[i] + pre[i - 1] + suf[i + 1]);
            }
        }

        return (res == INT_MAX) ? -1 : res;
    }
};
```







### 

