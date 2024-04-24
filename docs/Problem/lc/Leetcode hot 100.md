# Leetcode hot 100

## 哈希

### [1. 两数之和](https://leetcode.cn/problems/two-sum/)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        for (int i = 0; i < nums.size(); i++) {
            int aim = target - nums[i];
            if (hash.find(aim) != hash.end()) {
                return {hash[aim], i};
            }2 1 5 3 6 4 8 9 7
            else hash[nums[i]] = i;
        }
        return {};
    }
};
```



### [49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

```cpp
const int P = 131;

class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        // 对每个字符串进行sort后哈希
        unordered_map<string, int> hash;
        vector<vector<string>> ans;
        for (int i = 0; i < strs.size(); i++) {
            string temp = strs[i];
            sort(temp.begin(), temp.end());
            if (hash.find(temp) != hash.end()) {
                ans[hash[temp]].push_back(strs[i]);
            }
            else {
                ans.push_back({});
                hash[temp] = ans.size() - 1;
                ans[ans.size() - 1].push_back(strs[i]);
            }
        }
        return ans;
    }
};
```







### [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)



#### 2.16第一次做

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        // 如果需要在O(n)的时间内解决
        // 那么大概率只需要遍历一遍
        // 由于unordered_set内部基于哈希表实现，查找、插入和删除操作的平均时间复杂度是常数时间（O(1)）
        int ans = 0;
        unordered_set<int> hash;
        for (auto i : nums) hash.insert(i);
        for (auto x : nums) {
            if (hash.count(x) && !hash.count(x - 1)) {
                int y = x;
                hash.erase(x);
                while (hash.count(y + 1)) {
                    y++;
                    hash.erase(y);
                }
                ans = max(y - x + 1, ans);
            }
        }
        return ans;
    }
};
```



#### 2.17复习

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        // 由于我们想要得到的是连续的数字串
        // 那么实际上我们想要得到的是这个字符串的最小值
        // 这样我们可以通过遍历从这个最小值开始的字符串得到最长的长度

        // 需要注意的是原字符串中可能是有重复的数字的
        int res = 0;
        unordered_set<int> hash;
        if (nums.size() == 0) return 0;
        for (auto i : nums) hash.insert(i);
        for (auto i : nums) {
            int temp = 0;
            if (hash.count(i - 1)) {
                continue;
            }
            else {
                temp++;
                int x = i;
                while (hash.count(x + 1)) {
                    temp++;
                    x++;
                }
                res = max(temp, res);
            }
        }
        return res;
    }
};
```





## 双指针

### [283. Move Zeroes](https://leetcode.cn/problems/move-zeroes/)

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != 0) nums[j++] = nums[i];
        }
        for (; j < nums.size(); j++) nums[j] = 0;
    }
};
```



### 2.17第一次做

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        // 这是一道典型的双指针题目
        int i = 0, j = 0;
        for (; i < nums.size(); i++) {
            if (nums[i] == 0) {
                continue;
            }
            nums[j++] = nums[i];
        }
        while (j < nums.size()) {
            nums[j++] = 0;
        }
    }
};
```



### [11. Container With Most Water](https://leetcode.cn/problems/container-with-most-water/)

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int res = 0;
        int l = 0, r = height.size() - 1;
        while (l < r) {
            int hl = height[l], hr = height[r];
            res = max(res, (r - l) * min(hl, hr));
            printf("r: %d; l: %d; res: %d\n", r, l, res);
            if (height[l] < height[r] && l < r) l++;
            else if (height[l] >= height[r] && l < r) r--;
        }
        return res;
    }
};
```

#### 2.17第一次做

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        // 第一反应是两层循环，时间复杂度是0(n^2)
        // 优化：这是一个容器，所以可以是用双指针指向他的左右两边
        // 而指针如果需要向中间移动的话，并且还想要容积变大，那么移动之后的height必须要比移动之前的height高
        
        // 有左右两个容器壁，那么应该移动哪一个呢？
        // 移动较短的那根，才有可能提升容积的大小
        // 这样就能把所有的情况以O(n)的时间复杂度遍历一遍
        int res = 0;
        int i = 0, j = height.size() - 1;
        while (i < j) {
            int m = height[i], n = height[j];
            res = max(res, min(m, n) * abs(j - i));
            if (i < j && m < n) i++;
            else if (i < j && m >= n) j--;
        }
        return res;
    }
};
```



### [15. 3Sum](https://leetcode.cn/problems/3sum/)

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int j = i + 1, k = nums.size() - 1;
            for (; j < nums.size() - 1 && j < k; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                int sum = nums[i] + nums[j];
                while (nums[k] > -sum && k > j + 1) k--;
                if (nums[k] == -sum) ans.push_back({nums[i], nums[j], nums[k]});
            }
        }
        return ans;
    }
};
```

### [15. 3Sum](https://leetcode.cn/problems/3sum/)

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());
        int size = nums.size();
        for (int i = 0; i < size - 2; i++) {
            if (i > 0 && nums[i - 1] == nums[i]) continue;
            for (int j = i + 1, k = size - 1; j < k; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;
                while (j < k - 1 && nums[i] + nums[j] + nums[k - 1] >= 0) k--;
                if (nums[i] + nums[j] + nums[k] == 0) {
                    ans.push_back({nums[i], nums[j], nums[k]});
                }
            }
        }
        return ans;
    }
};
```



### [42. Trapping Rain Water](https://leetcode.cn/problems/trapping-rain-water/)



#### 2.20 前后缀分解

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0;
        int size = height.size();
        vector<int> left(size);
        vector<int> right(size);
        left[0] = height[0];
        right[size - 1] = height[size - 1];
        for (int i = 1; i < size; i++) {
            left[i] = max(height[i], left[i - 1]);
        }
        for (int i = size - 2; i >= 0; i--) {
            right[i] = max(height[i], right[i + 1]);
        }
        for (int i = 0; i < size; i++) {
            ans += min(left[i], right[i]) - height[i];
        }
        return ans;
    }
};
```





#### 2.20 单调栈

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        // 将接住雨水的面积横着看
        // 然后从左往右遍历，对于每根柱子右边能接住水的面积，取决于第一个大于等于它的x的差值，以及它和比他低的柱子y的差值
        // 思路：对于每次遍历到的值，要和他左边第二小的数去比
        stack<int> st;
        int ans = 0;
        for (int i = 0; i < height.size(); i++) {
            while (!st.empty() && height[i] > height[st.top()]) {
                int bottom = height[st.top()];
                st.pop();
                if (st.empty()) {
                    break;
                }
                int left = st.top();
                int dh = min(height[left], height[i]) - bottom;
                ans += dh * (i - left - 1);
            }
            st.push(i);
        }
        return ans;
        
    }
};
```





## 滑动窗口

### [3. Longest Substring Without Repeating Characters](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

#### 2.20第一次尝试

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() == 0) return 0;
        // vector<int> record(26);
        unordered_map<char, int> hash;
        
        int left = 0, right = 0;
        
        int res = 1;
        for (; left <= right && right < s.size(); right++) {
            hash[s[right]]++;
            while (hash[s[right]] > 1 && left < right) {
                hash[s[left]]--;
                left++;
            }
            cout << right << " " << left << endl;
            res = max(res, right - left + 1);
        }
        return res;
    }
};
```



### [438. Find All Anagrams in a String](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

#### 2.20第一次尝试

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> ans;
        vector<int> record(26);
        if (s.size() == 0 || p.size() == 0) return ans;
        for (int i = 0; i < p.size(); i++) {
            record[p[i] - 'a']++;
        }
        int left = 0, right = 0;
        for (; left <= right && right < s.size(); right++) {
            record[s[right] - 'a']--;
            while (record[s[right] - 'a']  < 0 && left <= right) {
                record[s[left] - 'a']++;
                left++;
            }
            if (right - left + 1 == p.size()) ans.push_back(left);
        }
        return ans;
    }
};
```





## 子串



### [560. Subarray Sum Equals K](https://leetcode.cn/problems/subarray-sum-equals-k/)

#### 2.20暴力做法，答案正确但是无法通过

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        // 一开始的想法是滑动窗口，但是发现nums中可以有负数，那么就不能使用滑动窗口了
        // 是典型的前缀和问题
        // 首先使用暴力做法，每个字母作为开头进行遍历
        // 超时了...
        int res = 0;
        for (int i = 0; i < nums.size(); i++) {
            int sum = 0;
            for (int j = i; j < nums.size(); j++) {
                sum += nums[j];
                if (sum == k) res++;
            }
        }
        return res;
    }
};
```



#### 2.20第一次做，值得重新做

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        // 关键在于使用前缀和，并且想到用sum[i] - k在哈希表中进行查找
        int res = 0;
        int n = nums.size();
        vector<int> sum(n + 1);
        unordered_map<int, int> hash;
        hash[0] = 1;
        for (int i = 1; i <= n; i++) {
            sum[i] = sum[i - 1] + nums[i - 1];
        }
        for (int i = 1; i <= n; i++) {
            if (hash.count(sum[i] - k)) {
                res += hash[sum[i] - k];
            }
            hash[sum[i]]++;
        }
        return res;
    }
};
```





### [239. Sliding Window Maximum](https://leetcode.cn/problems/sliding-window-maximum/)

#### 2.20第一次做，值得重做

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        // 分析滑动窗口的思路
        // 滑动窗口分为加入新的，然后删除旧的
        // 新的加进来如果是小数，那么它未来仍然有可能成为最大值
        // 新加进来的如果是大数，那么既然他已经在k个里面了，那么它左侧的所有比他小的数应该删除
        // 滑动窗口吐出的必须是一个最大值

        // 在我们的队列里面必须要保证是单调递减的
        vector<int> res;
        deque<int> q;
        for (int i = 0; i < nums.size(); i++) {
            // 先出队列
            if (q.size() && q.front() + k - 1 < i) q.pop_front();
            // 然后进队列前，将左边小于新的数的所有数都删除
            while (q.size() && nums[q.back()] <= nums[i]) q.pop_back();
            // 加入新的数
            q.push_back(i);
            // 记录最大值
            if (i >= k - 1) res.push_back(nums[q.front()]);
        }
        return res;
    }
};
```



### [76. Minimum Window Substring](https://leetcode.cn/problems/minimum-window-substring/)



### 2.21 第一次尝试，麻烦，值得做第二次

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map <char, int> hash;
        for (char c : t) {
            hash[c]++;
        }
        int total = hash.size();
        int l = 0, r = INT_MAX;
        for (int left = 0, right = 0; right < s.size(); right++) {
            if (--hash[s[right]] == 0) {
                total--;
            }
            // // 当前窗口已包含所有字符,找出符合条件的最小值
            while (total == 0) {
                if ((right - left) < (r - l)) {
                    r = right;
                    l = left;
                }
                if (hash.count(s[left]) && ++hash[s[left]] > 0) {
                    total++;  // 缩小窗口直到不再满足条件
                }
                left++;
            }
        }
        if (r - l == INT_MAX) return "";
        else return s.substr(l, r - l + 1);
    }
};
```







### 原答案

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        // 需要使用total 来记录还需要匹配的字符种类数
        // vector<int> c1(60), c2(60);
        // 同样的字母只要c1中的比c2中的大，那么指针就可以更新
        // a-z对应0-25，A-Z对应26-51
        int m = s.size(), n = t.size();
        vector<int> c1(60), c2(60);
        int total = 0;
        int min = INT_MAX;
        string ans;
        for (char ch : t) {
            if (++c2[getId(ch)] == 1) {
                total++;
            }
        }
        for (int i = 0, j = 0; i < m; i++) {
            if (++c1[getId(s[i])] == c2[getId(s[i])]) {
                total--;
            }
            while (j < i) {
                int idx2 = getId(s[j]);
                if (c1[idx2] > c2[idx2]) {
                    --c1[idx2];
                    j++;
                }
                else break;
            }
            if (total == 0 && (ans.empty() || ans.length() > i - j + 1)) ans = s.substr(j, i - j + 1);

        }
        return ans;

    }
    int getId(char ch) {
        return ch >= 'A' && ch <= 'Z' ? ch - 'A' + 26 : ch - 'a';
    }
    
};
```





## 普通数组



### [53. Maximum Subarray](https://leetcode.cn/problems/maximum-subarray/)

#### 2.21第一次做， 前缀和做法

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        // 子数组的和想到使用前缀和来做
        int pre_sum = 0;
        int ans = INT_MIN;
        int min_pre_sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            pre_sum += nums[i];
            ans = max(ans, pre_sum - min_pre_sum);
            min_pre_sum = min(min_pre_sum, pre_sum);
        }
        return ans;
    }
};
```



#### 2.21第一次做，动态规划做法

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        // 这个子串问题实际上也是选或者不选的问题，选nums[i - 1]结尾的最大的值或者选0
        // dp[i]表示以nums[i]结尾的最大的值
        // dp[i] = max(dp[i - 1], 0) + nums[i]
        // 由于是一维dp，如果选dp[i - 1]就是连续的子串，选0就是不要前面的子串
        vector<int> dp(nums.size());
        dp[0] = nums[0];
        int res = dp[0];
        for (int i = 1; i < nums.size(); i++) {
            dp[i] = max(dp[i - 1], 0) + nums[i];
            if (dp[i] > res) res = dp[i];
        }
        return res;
    }
};
```



#### 2.21第一次做使用了分治的思想+线段树

```cpp
class Solution {
public:
    struct Status {
        int lSum, rSum, mSum, iSum;
    };

    Status pushUp(Status l, Status r) {
        int iSum = l.iSum + r.iSum;
        int lSum = max(l.lSum, l.iSum + r.lSum);
        int rSum = max(r.rSum, r.iSum + l.rSum);
        int mSum = max(max(l.mSum, r.mSum), l.rSum + r.lSum);
        return (Status) {lSum, rSum, mSum, iSum};
    }

    Status get(vector<int> &a, int l, int r) {
        if (l == r) {
            return (Status) {a[l], a[l], a[l], a[l]};
        }
        int m = (l + r) >> 1;
        Status lSub = get(a, l, m);
        Status rSub = get(a, m + 1, r);
        return pushUp(lSub, rSub); 
    }
    int maxSubArray(vector<int>& nums) {
        // 使用分治做法
        // lsum表示[l, r]内以l为左端点的最大子段和
        // rsum表示[l, r]内以r为右端点的最大子段和
        // msum表示[l, r]内最大的子段和
        // isum表示[l, r]的区间和
        
        // ---------------------------------------------
        // lsum：1. 左子区间的lsum 2. 左子区间的isum + 右子区间的lsum
        // rsum: 2. 右子区间的rsum 2. 右子区间的isum + 左子区间的rsum
        // isum: 左子区间的isum+右子区间的isum
        // msum：1. 左子区间的msum 2. 右子区间的msum 3. 左子区间的rsum + 右子区间的lsum
        return get(nums, 0, nums.size() - 1).mSum;
    }
};
```





### [56. Merge Intervals](https://leetcode.cn/problems/merge-intervals/)

#### 2.22 第一次做，注意sort的用法，并且`vector<int>`用empty(),`vector<vector<int>>` 可以用.back()

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.empty()) return {};
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        for (auto& i : intervals) {
            if (ans.empty() || ans.back()[1] < i[0]) {
                ans.push_back(i);
            }
            else {
                ans.back()[1] = max(ans.back()[1], i[1]);
            }
        }
        return ans;
    }
};
```



### [89. Rotate Array](https://leetcode.cn/problems/rotate-array/)



#### 2.22第一次做 reverse方法，注意对vector实际上是可以直接reverse的

```cpp
class Solution {
public:
    void reverse(vector<int>& nums, int l, int r) {
        int m = l, n = r;
        while (m < n) {
            int temp = nums[m];
            nums[m] = nums[n];
            nums[n] = temp;
            m++;
            n--;
        }
    }
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n;
        reverse(nums, 0, n - 1);        
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }
};
```



### 2.22 第一次做需要额外空间的方法，不推荐

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> ans(nums.size());
        for (int i = 0; i < nums.size(); i++) {
            ans[(i + k) % nums.size()] = nums[i];
        }
        for (int i = 0; i < nums.size(); i++) {
            nums[i] = ans[i];
        }

    }
};
```



### [238. Product of Array Except Self](https://leetcode.cn/problems/product-of-array-except-self/)



#### 2.24 第一次做，使用前后缀分解，一开始没有想到



```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        // 使用前后缀分解
        // 需要想到这道题目实际上就是左边的乘积乘上右边的乘积
        // 那么分别从左往右和从右往左维护两个乘积数组即可
        int n = nums.size();
        vector<int> left(n), right(n);
        left[0] = nums[0];
        right[n - 1] = nums[n - 1];
        for (int i = 1; i < n; i++) {
            left[i] = left[i - 1] * nums[i];
        }
        for (int i = n - 2; i >= 0; i--) {
            right[i] = right[i + 1] * nums[i];
        }
        vector<int> ans(n);
        ans[0] = right[1];
        ans[n - 1] = left[n -2];
        for (int i = 1; i <= n - 2; i++) {
            ans[i] = left[i - 1] * right[i + 1];
        }
        return ans;

    }
};
```



#### 2.22 第一次做，优化空间复杂度

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        // 为什么说可以优化空间复杂度：返回的数组是不算在空间复杂度里面的
        // 所以需要将left和right数组给优化掉
        int n = nums.size();
        vector<int> ans(n);
        ans[0] = 1;
        for (int i = 1; i < n; i++) {
            // 用ans来作为left数组
            ans[i] = ans[i - 1] * nums[i - 1];
        }
        // 用一个变量来地带存储right数组
        int right = 1;
        for (int i = n - 1; i >= 0; i--) {
            ans[i] = ans[i] * right;
            right *= nums[i];
        }
        return ans;

        
    }
};
```



### [41. First Missing Positive](https://leetcode.cn/problems/first-missing-positive/)



#### 2.22 第一次做，困难题的难点在于思考

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        // 第一反应是将所有数全部插入到哈希表中，然后从头进行查询即可
        // unordered_set<int> hash;
        // for (auto n : nums) hash.insert(n);
        // int res = 1;
        // while (hash.find(res) != hash.end()) res++;
        // return res;
        // ---------------------------------------------------
        
        // 这道题目使用O(1)空间复杂度的关键点在于只使用原数组的位置
        // 最重要的是看出长度为n的数组中缺失的最小的正整数必然在1-n+1之间
        // 既然如此，我们将nums[0]~nums[n - 1]分别对应1~n即可，然后从头遍历，第一个nums[i] != i + 1的数就是答案
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            while (nums[i] >= 1 && nums[i] < n && nums[i] != i + 1 && nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }
        return n + 1;
    }
};
```



## 矩阵



### [73. Set Matrix Zeroes](https://leetcode.cn/problems/set-matrix-zeroes/)

#### 2.23第一次做 真无聊的题目



```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        vector<int> row(matrix.size(), 1);
        vector<int> col(matrix[0].size(), 1);
        for (int i = 0; i < matrix.size(); i++) {
            for (int j = 0; j < matrix[0].size(); j++) {
                if (matrix[i][j] == 0) {
                    row[i] = 0;
                    col[j] = 0;
                }
                
            }
        }
        for (int i = 0; i < matrix.size(); i++) {
            for (int j = 0; j < matrix[0].size(); j++) {
                if (row[i] == 0 || col[j] == 0) matrix[i][j] = 0;
            }
        }
    }
};
```





#### 2.23 第一次做 优化了空间到O(1)

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        // 优化到每一行每一列的第一个数字用来记录这行是否需要被刷成0
        // 由于第一行和第一列本身可能没有0并不需要整行整列被刷成0
        // 所以需要额外的两个bool变量来记录第一行和第一列是否需要被刷成0
        bool row0 = false, col0 = false;
        int m = matrix.size(), n = matrix[0].size();
        for (int i = 0; i < n; i++) {
            if (matrix[0][i] == 0) row0 = true;
        }
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) col0 = true;
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (row0) {
            for (int i = 0; i < n; i++) {
                matrix[0][i] = 0;
            }
        }
        if (col0) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
};
```



### [54. Spiral Matrix](https://leetcode.cn/problems/spiral-matrix/)

#### 2.23 第一次做，注意将复杂的表达式先用变量记录下来

``` cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans;
        int dx[4] = {1, 0, -1, 0}, dy[4] = {0, 1, 0, -1};  // Direction vectors for right, down, left, up
        int dimension = 0;  // To keep track of the current direction
        int m = matrix.size(), n = matrix[0].size();  // Dimensions of the matrix
        vector<vector<int>> visited(m, vector<int>(n, 0));  // To keep track of visited elements

        for (int i = 0, x = 0, y = 0; i < m * n; i++) {
            ans.push_back(matrix[y][x]);  // Add the current element to the answer
            visited[y][x] = 1;  // Mark the current element as visited

            // Calculate the next position
            int nx = x + dx[dimension];
            int ny = y + dy[dimension];

            // Check if the next position is within bounds and not visited
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && visited[ny][nx] == 0) {
                x = nx;
                y = ny;
            } else {
                // Change direction
                dimension = (dimension + 1) % 4;
                x += dx[dimension];
                y += dy[dimension];
            }
        }

        return ans;
    }
};

```



### [48. Rotate Image](https://leetcode.cn/problems/rotate-image/)

#### 2.23第一次做需要想到顺时针90度旋转 = 先沿着左上右下对称一次 + 左右沿中轴线对称一次

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        // 如果可以allocate another 2D matrix，直接新建一个扫描即可
        // 顺时针90度旋转 = 先沿着左上右下对称一次 + 左右沿中轴线对称一次
        int n = matrix.size();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                swap(matrix[i][j], matrix[i][n - j - 1]);
            }
        }

    }
};
```



### [240. Search a 2D Matrix II](https://leetcode.cn/problems/search-a-2d-matrix-ii/)

#### 2.23 第一次做,Z字搜索

```cpp
```



## 链表

### [160. Intersection of Two Linked Lists](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

#### 2.24第一次做，但是应该不是题意的意思

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        // 假设有交集，那么后半段一定是一样的
        // 第一次将长度跑出来m, n
        // 然后让长的先走(m - n)个，然后再一起往前走即可
        ListNode *a = headA, *b = headB;
        int ca = 1, cb = 1;
        while (a != NULL && a->next != NULL) {
            ca++;
            a = a->next;
        }
        while (b != NULL && b->next != NULL) {
            cb++;
            b = b->next;
        }
        if (cb > ca) {
            ListNode *temp = headA;
            headA = headB;
            headB = temp;
        }
        int count = abs(ca - cb);
        a = headA, b = headB;
        while (count) {
            a = a->next;
            count--;
        }
        while (a != b) {
            a = a->next;
            b = b->next;
        }
        return a;
    }
};
```



#### 2.24第一次做，哈希表方法不够简洁

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        // 哈希表
        unordered_set<ListNode *> visited;
        ListNode *temp = headA;
        while (temp != NULL) {
            visited.insert(temp);
            temp = temp->next;
        }
        temp = headB;
        while (temp != NULL) {
            if (visited.count(temp)) {
                return temp;
            }
            temp = temp->next;
        }
        return nullptr;
    }
};
```



#### 2.24第一次做，双指针法+两个指针同时走过m + n的长度思路

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        // 既然两个头走过的路分别是m和n，所以会不相交
        // 那么让两个头都走过m + n，那他们在后半段必然相交

        // 这个方法实际上是双指针
        if (headA == nullptr && headB == nullptr) return nullptr;
        ListNode *pa = headA, *pb = headB;
        while (pa != pb) {
            pa = pa == nullptr ? headB : pa->next;
            pb = pb == nullptr ? headA : pb->next;
        }
        return pa;
    }
};
```



### [206. Reverse Linked List](https://leetcode.cn/problems/reverse-linked-list/)

#### 2.24第一次做，很常规很简单

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
    ListNode* reverseList(ListNode* head) {
        // 1->2->3
        if (head == nullptr) return head;
        ListNode *tmp = head, *prev = nullptr;
        while (tmp != nullptr) {
            ListNode *next = tmp->next;
            tmp->next = prev;
            prev = tmp;
            tmp = next;
        }
        head = prev;
        return head;
    }
};
```











#### 原答案

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
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = NULL;
        ListNode* curr = head;
        while (curr != nullptr) {
            ListNode* tmp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = tmp;
        }
        return prev;
    }
};
```



### [234. Palindrome Linked List](https://leetcode.cn/problems/palindrome-linked-list/)

#### 2.24第一次做，递归是最好的方法，值得多次做

如果使用递归反向迭代节点，同时使用递归函数外的变量向前迭代，就可以判断链表是否为回文。

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
    ListNode *frontPointer;
public:
    bool recursivelyCheck(ListNode* curr) {
        if (curr != nullptr) {
            if (!recursivelyCheck(curr->next)) {
                return false;
            }
            if (curr->val != frontPointer->val) {
                return false;
            }
            frontPointer = frontPointer->next;
        }
        return true;
    }
    bool isPalindrome(ListNode* head) {
        frontPointer = head;
        return recursivelyCheck(head);
    }
};
```



#### 2.24 第一次做，快慢指针还行

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if (head == nullptr) {
            return true;
        }

        // 找到前半部分链表的尾节点并反转后半部分链表
        ListNode* firstHalfEnd = endOfFirstHalf(head);
        ListNode* secondHalfStart = reverseList(firstHalfEnd->next);

        // 判断是否回文
        ListNode* p1 = head;
        ListNode* p2 = secondHalfStart;
        bool result = true;
        while (result && p2 != nullptr) {
            if (p1->val != p2->val) {
                result = false;
            }
            p1 = p1->next;
            p2 = p2->next;
        }        

        // 还原链表并返回结果
        firstHalfEnd->next = reverseList(secondHalfStart);
        return result;
    }

    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;
        while (curr != nullptr) {
            ListNode* nextTemp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }

    ListNode* endOfFirstHalf(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast->next != nullptr && fast->next->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
    }
};

```



#### 2.24第一次做，建一个数组得方法，不推荐



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
    bool isPalindrome(ListNode* head) {
        vector<int> val;
        ListNode* tmp = head;
        while (tmp != nullptr) {
            val.push_back(tmp->val);
            tmp = tmp->next;
        }
        for (int i = 0, j = val.size() - 1; i < j; i++, j--) {
            if (val[i] != val[j]) return false;
        }
        return true;
    }
};
```







### [141. Linked List Cycle](https://leetcode.cn/problems/linked-list-cycle/)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == nullptr) return false;
        ListNode *fast = head, *slow = head;
        while (fast->next != nullptr && fast->next->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) return true;
        }
        return false;
    }
};
```









#### 原答案

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode *fast = head;
        ListNode *slow = head;
        // 使用快慢指针的时候，如果fast+2,slow+1，那么实际上每次追及的距离就是1，不用担心fast会超过slow
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) return true; // 要在每次移动指针后比较是否追及成功
        }
        return false;
    }
};
```



### [142. Linked List Cycle II](https://leetcode.cn/problems/linked-list-cycle-ii/)

#### 2.24第一次做，已经好多次了不难，主要是分析

#### 原答案

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        // 如果只有一个环，那么快指针是慢指针两倍的话，会相遇在最初的起点
        // 而有了非环的部分，会相遇在慢指针还没走完一圈的时候
        // 快指针走过的路= a + n(b + c) +b
        // 慢指针走过的路= a + b
        // 2a + 2b = a + (n + 1) b + nc
        // a = (n - 1)b + (n - 1)c + c
        // 如果head和慢指针同时走a的路，那么head会到入环点，而慢指针会在转了(k - 1)圈之后到入环点
        ListNode *fast = head, *slow = head;
        while (true) {
            if (fast == nullptr || fast->next == nullptr) return nullptr;
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) break;
        }
        ListNode *curr = head;
        while (curr != fast) {
            fast = fast->next;
            curr = curr->next;
        }
        return curr;
    }
};
```







### [21. Merge Two Sorted Lists](https://leetcode.cn/problems/merge-two-sorted-lists/)

#### 2.24第一次做，递归，最好的做法，最精妙的做法

链表问题不要忘记递归

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
        if (list1 == nullptr) return list2;
        if (list2 == nullptr) return list1;
        if (list1->val <= list2->val) {
            list1->next = mergeTwoLists(list1->next, list2);
            return list1;
        }
        list2->next = mergeTwoLists(list1, list2->next);
        return list2;
    }
};
```





#### 2.24第一次做迭代，迭代并不是这道题最精妙的思考方式

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
        ListNode* dummy = new ListNode(-1);
        ListNode* curr = dummy;
        while (list1 != nullptr && list2 != nullptr) {
            if (list1->val < list2->val) {
                curr->next = list1;
                list1 = list1->next;
                curr = curr->next;
            }
            else {
                curr->next = list2;
                list2 = list2->next;
                curr = curr->next;
            }
        }
        if (list1 != nullptr) curr->next = list1;
        if (list2 != nullptr) curr->next = list2;
        return dummy->next;
    }
};
```



### [2. Add Two Numbers](https://leetcode.cn/problems/add-two-numbers/)

#### 2.24第一次做会做

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
        ListNode *dummy = new ListNode(-1), *curr = dummy;
        int add = 0;
        while (l1 || l2 || add) {
            int sum = add;
            if (l1) sum += l1->val;
            if (l2) sum += l2->val;
            curr->next = new ListNode(sum % 10, nullptr);
            add = sum / 10;
            curr = curr->next;
            if (l1) l1 = l1->next;
            if (l2) l2 = l2->next;
        }
        return dummy->next;
    }
};
```



#### 原答案

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



### [19. Remove Nth Node From End of List](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

#### 2.25第一次做，很简单

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
        // 既然要去掉尾部的第n个，那么可以使用双指针
        // 让快指针先运行n步
        if (!head) return head;
        ListNode *dummy = new ListNode(-1, head);
        ListNode *fast = dummy, *slow = dummy;
        for (int i = 0; i < n; i++) {
            fast = fast->next;
        }
        while (fast && fast->next) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy->next;
    }
};
```



#### 原答案

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
        ListNode* dummy = new ListNode(-1, head);
        ListNode *right = dummy, *left = dummy;
        for (int i = 0; i < n; i++) {
            right = right->next;
        }
        while (right->next != nullptr) {
            right = right->next;
            left = left->next;
        }
        left->next = left->next->next;
        return dummy->next;
    }
};
```



### [24. Swap Nodes in Pairs](https://leetcode.cn/problems/swap-nodes-in-pairs/)

#### 2.25第一次尝试，用了三个ListNode暴力解了，可以有一个ListNode的方法

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
        if (!head) return head;
        ListNode *dummy = new ListNode(-1, head);
        ListNode *curr = dummy;
        while (curr && curr->next && curr->next->next) {
            ListNode *first = curr->next;
            ListNode *second = curr->next->next;
            ListNode *third = curr->next->next->next;
            curr->next = second;
            second->next = first;
            first->next = third;
            curr = curr->next->next;
        }
        return dummy->next;
    }
};
```



#### 2.25第一次做，只用一个额外ListNode 的方法

思考方法：能和第一个node以及后面连上的node都可以产生直接联系的是第二个node

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
        if (!head) return head;
        ListNode *dummy = new ListNode(-1, head);
        ListNode *curr = dummy;
        while (curr && curr->next && curr->next->next) {
            ListNode *tmp = curr->next->next;
            curr->next->next = tmp->next;
            tmp->next = curr->next;
            curr->next = tmp;
            curr = curr->next->next;
        }
        return dummy->next;
    }
};
```





#### 原答案

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
        ListNode* dummy = new ListNode(-1, head);
        ListNode* curr = dummy;
        while (curr && curr->next && curr->next->next) {
            ListNode* tmp = curr->next->next;
            curr->next->next = tmp->next;
            tmp->next = curr->next;
            curr->next = tmp;
            curr = curr->next->next;
        }
        return dummy->next;
    }
};
```





### [25. Reverse Nodes in k-Group](https://leetcode.cn/problems/reverse-nodes-in-k-group/)



#### 2.25第一次做，纯暴力做法，和原答案几乎一个意思

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
        ListNode *dummy = new ListNode(-1, head);
        ListNode *curr = dummy;
        while (curr) {
            ListNode *tmp = curr;
            for (int i = 0; i < k; i++) {
                tmp = tmp->next;
                if (!tmp) return dummy->next;
            }

            ListNode *left = curr->next, *right = curr->next->next;
            for (int i = 0; i < k - 1; i++) {
                ListNode *third = right->next;
                right->next = left;
                left = right;
                right = third;
            }
            curr->next->next = right;
            curr->next = left;



            for (int i = 0; i < k; i++) {
                curr = curr->next;
            }
        }
        return dummy->next;
    }
};
```





#### 原答案

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
        ListNode *dummy = new ListNode(-1, head);
        dummy->next = head;
        for (auto p = dummy; ;) {
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
            p = c; // 注意翻转了之后，前k个节点中的第一个变成了最后一个，也变成了下一个k节点的前一个节点！
        }
        return dummy->next;
    }
};
```





### [138. Copy List with Random Pointer](https://leetcode.cn/problems/copy-list-with-random-pointer/)



#### 2.26第一次做，回溯+哈希表

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
    // 使用回溯+哈希表
public:
    unordered_map<Node*, Node*> cacheNode;
    Node* copyRandomList(Node* head) {
        if (head == NULL) return NULL;
        else if (cacheNode.count(head)) {
            return cacheNode[head];
        }
        else {
            Node* newNode = new Node(head->val);
            cacheNode[head] = newNode;
            newNode->next = copyRandomList(head-a>next);
            newNode->random = copyRandomList(head->random);
            return newNode;
        }
    }
};
```



#### 2.26 第一次做纯暴力，过于丑陋了

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, int> hash;
        vector<Node*> nodeList;
        Node* dummy = new Node(-1);
        Node* curr = head;
        Node* currCopy = dummy;
        int i = 0;
        while (curr) {
            Node* tmp = new Node(curr->val);
            hash[curr] = i;
            nodeList.push_back(tmp);
            currCopy->next = tmp;
            currCopy = currCopy->next;
            curr = curr->next;
            i++;
        }
        
        currCopy->next = NULL;
        currCopy = dummy->next;
        curr = head;
        while (curr) {;
            if (curr->random == NULL) {
                currCopy->random = NULL;
            }
            else {
                int i = hash[curr->random];
                currCopy->random = nodeList[i];
            }
            curr = curr->next;
            currCopy = currCopy->next;
        }
        return dummy->next;
    }
};
```





### [148. 排序链表](https://leetcode.cn/problems/sort-list/)

#### 3.3第一次做,非常好也非常难的题目，可以多次做

只能使用归并排序自底向上做

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
    ListNode* sortList(ListNode* head) {
        int n = 0;
        for (auto p = head; p; p = p->next) n++;
        auto dummy = new ListNode(-1);
        dummy->next = head;

        for (int i = 1; i < n; i *= 2) {
            auto curr = dummy;
            for (int j = i; j <= n; j += 2 * i) {
                auto p = curr->next;
                auto q = p;
                for (int k = 0; k < i; k++) q = q->next;
                int x = 0, y = 0;
                while (x < i && y < i && p && q) {
                    if (p->val <= q->val) {
                        curr->next = p;
                        curr = curr->next;
                        p = p->next;
                        x++;
                    }
                    else {
                        curr->next = q;
                        curr = curr->next;
                        q = q->next;
                        y++;
                    }
                }
                while (x < i && p) {
                    curr->next = p;
                    curr = curr->next;
                    p = p->next;
                    x++;
                }
                while (y < i && q) {
                    curr->next = q;
                    curr = curr->next;
                    q = q->next;
                    y++;
                }
                curr->next = q;
            }
            
        }
        return dummy->next;
    }
};
```





#### 快速排序模板

```cpp
#include <iostream>
using namespace std;
int n;

void quick_sort(int q[], int l, int r) {
    if (r <= l) return;
    int i = l - 1, j = r + 1;
    int x = q[l + r >> 1];
    while (i  < j) {
        do i++; while (q[i] < x);
        do j--; while (q[j] > x);
        if (i < j) swap(q[i], q[j]);
    }
    quick_sort(q, l, j);
    quick_sort(q, j + 1, r);
}

int main () {
    scanf("%d", &n);
    int q[n];
    for (int i = 0; i < n; i++) scanf("%d", &q[i]);
    quick_sort(q, 0, n - 1);
    for (int i = 0; i < n; i++) printf("%d ", q[i]);
    return 0;
}
```





### [23. 合并 K 个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

#### 3.3 第一次做，很好的题目

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
    ListNode* mergeTwoLists(ListNode* a, ListNode* b) {
        ListNode* dummy = new ListNode(-1), *curr = dummy;
        while (a && b) {
            if (a->val < b->val) {
                curr->next = a;
                curr = curr->next;
                a = a->next;
            }
            else {
                curr->next = b;
                curr = curr->next;
                b = b->next;
            }
        }
        curr->next = a ? a : b;
        return dummy->next;
    }
    ListNode* merge(vector<ListNode *>& lists, int l, int r) {
        if (l == r) return lists[l];
        if (l > r) return nullptr; 
        int mid = l + r >> 1;
        return mergeTwoLists(merge(lists, l, mid), merge(lists, mid + 1, r));
    }

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        // 归并排序，自底向上迭代归并
        // 并且需要将数组和链表的归并排序分开来
        int n = lists.size();
        if (n == 0) return nullptr;
        return merge(lists, 0, n - 1);
    }
};
```











#### 原答案

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







### [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)

快速插入一个节点

快速删除一个节点

并使得这两个操作的时间复杂度都为O(1)



单链表不能再O(1)的时间删除,所以需要双链表

双链表再定义的时候需要用到左右两个端点

#### 3.3第一次做,很好的LRU题目



```cpp
class LRUCache {
public:
    // 双链表
    struct Node {
        int key, value;
        Node* left, *right;
        Node(int key, int value) : key(key), value(value), left(nullptr), right(nullptr) {}
    } *L, *R;
    // 哈希表
    unordered_map<int, Node*> hash;
    //  缓存大小
    int n = 0;
    LRUCache(int capacity) {
        n = capacity;
        // 初始化双链表
        L = new Node(-1, -1), R = new Node(-1, -1);
        L->right = R;
        R->left = L;
    }
    
    int get(int key) {
        // 查询哈希表
        // 在
        if (hash.count(key) == 1) {
            Node* p = hash[key];
            remove(p);
            insert(p);
            return p->value;
        }
        // 不在
        return -1;
    }
    
    void put(int key, int value) {
        // 在
        if (hash.count(key) == 1) {
            Node* p = hash[key];
            p->value = value;
            remove(p);
            insert(p);
        }
        // 不在
        else {
            if (hash.size() == n) {
                Node* p = R->left;
                // 删除双链表
                remove(p);
                // 删除哈希表
                hash.erase(p->key);
                // 删除内存
                delete(p);
            }
            Node* p = new Node(key, value);
            insert(p);
            hash[key] = p;
        }
    }

    void remove(Node* p) {
        p->left->right = p->right;
        p->right->left = p->left;
    }

    void insert(Node* p) {
        p->right = L->right;
        p->left = L;
        L->right = p;
        p->right->left = p;
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```





## 二叉树

### [94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

#### 3/4第一次做，忘记中序遍历是什么了

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root, res);
        return res;
    }
    void inorder(TreeNode* root, vector<int> & res) {
        if (!root) return;
        inorder(root->left, res);
        res.push_back(root->val);
        inorder(root->right, res);
    }
};
```





### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

#### 3/4第一次做

 ```cpp
 /**
  * Definition for a binary tree node.
  * struct TreeNode {
  *     int val;
  *     TreeNode *left;
  *     TreeNode *right;
  *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
  *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
  *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
  * };
  */
 class Solution {
 public:
     int res = 0;
     int maxDepth(TreeNode* root) {
         inorder(root, 1);
         return res;
     }
     void inorder(TreeNode* root, int depth) {
         if (!root) return;
         inorder(root->left, depth + 1);
         res = max(depth, res);
         inorder(root->right, depth + 1);
     }
 
 };
 ```







#### 原答案

````cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    // ans这里是Solution这个类的成员变量，在整个Solution的生命周期中一直存在
    // 所以ans这里相当于Solution中的全局变量
    // 实现了多次调用 dfs 函数的过程中累积并维护一个全局的最大深度值
    int ans = 0;
    void dfs(TreeNode *node, int count) {
        if (node == nullptr) return;
        count++;
        ans = max(ans, count);
        dfs(node->left, count);
        dfs(node->right, count);
    }
public:
    int maxDepth(TreeNode* root) {
        dfs(root, 0);
        return ans;
    }
};
````



### [226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

#### 3/4第一次做想不出来递归的做法

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        // 使用的是递归的思想
        if (!root) return nullptr;
        TreeNode* left = invertTree(root->left);
        TreeNode* right = invertTree(root->right);
        root->left = right;
        root->right = left;
        return root;
    }
};
```





### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

#### 3/4第一次值得第二次做

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool checkSymmetric(TreeNode* a, TreeNode* b) {
        if (a == nullptr || b == nullptr) return a == b;
        return (a->val == b->val) && (checkSymmetric(a->left, b->right)) && (checkSymmetric(a->right, b->left));
    }
    bool isSymmetric(TreeNode* root) {
        return checkSymmetric(root->left, root->right);
    }
};
```





#### 原答案

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    bool check(TreeNode *a, TreeNode *b) {
        if (a == nullptr || b == nullptr) return a == b;
        return (a->val == b->val) && check(a->left, b->right) && check(a->right, b->left);
    }
public:

    bool isSymmetric(TreeNode* root) {
        return check(root->left, root->right);
    }
};
```





### [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

#### 3/4第一次做

 ```cpp
 /**
  * Definition for a binary tree node.
  * struct TreeNode {
  *     int val;
  *     TreeNode *left;
  *     TreeNode *right;
  *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
  *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
  *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
  * };
  */
 class Solution {
 public:
     int res = 0;
     int diameterOfBinaryTree(TreeNode* root) {
         maxDepth(root);
         return res;
     }
     int maxDepth(TreeNode* root) {
         // 每次返回接收到的都是最大深度
         if (!root) return 0;
         int left = maxDepth(root->left);
         int right = maxDepth(root->right);
         int sum = left + right;
         res = max(sum, res);
         return max(left, right) + 1;
     }
 };
 ```





### [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)



#### 3/4优雅使用队列

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            vector<int> vals;
            int n = q.size();
            while (n--) {
                auto node = q.front();
                q.pop();
                vals.push_back(node->val);
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            ans.emplace_back(vals);
        }
        return ans;
    }
};
```





#### 3/4自己的做法，两个数组，不够优雅

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) return {};
        vector<TreeNode*> level;
        level.push_back(root);
        while (!level.empty()) {
            vector<int> tmp;
            for (int i = 0; i < level.size(); i++) tmp.push_back(level[i]->val);
            ans.push_back(tmp);
            lOrder(level);
        }
        return ans;
    }
    void lOrder(vector<TreeNode*>& level) {
        vector<TreeNode*> tmp;
        for (auto n : level) {
            if (n->left) tmp.push_back(n->left);
            if (n->right) tmp.push_back(n->right);
        }
        level = tmp;
    }
    
};
```





### [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

#### 3/4第一次做，没有做错一次过

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        // 二分搜索即可
        return binarySearchBST(nums, 0, nums.size() - 1);
    }

    TreeNode* binarySearchBST(vector<int>& nums, int l, int r) {
        if (l > r) return nullptr;
        int mid = l + r >> 1;
        TreeNode* newNode = new TreeNode(nums[mid]);
        if (l == r) return newNode;
        newNode->left = binarySearchBST(nums, l, mid - 1);
        newNode->right = binarySearchBST(nums, mid + 1, r);
        return newNode;
    }

};
```



#### 原答案

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        TreeNode* res = build(nums, 0, nums.size() - 1);
        return res;
    }
    TreeNode* build(vector<int>& nums, int l, int r) {
        if (l > r) return NULL;
        int mid = (l + r) >> 1;
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = build(nums, l, mid - 1);
        root->right = build(nums, mid + 1, r);
        return root;
    }
};
```





### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)



#### 3/4第一次做，使用二叉搜索树的性质，建议多做

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    // 一定要注意使用二叉搜索树的性质：中序遍历是递增数列
public:
    TreeNode* pre;
    bool isValidBST(TreeNode* root) {
        if (!root) return true;
        bool left = isValidBST(root->left);
        if (pre && pre->val >= root->val) return false;
        pre = root;
        bool right = isValidBST(root->right);
        return left && right;
    }
};
```





#### 3/4第一次做，不够优雅

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        // 仅验证每个节点大于它的两个子节点是不完备的
        return checkBST(root, LLONG_MIN, LLONG_MAX);
    }
    bool checkBST(TreeNode* root, long long l, long long r) {
        if (!root) return true;
        int value = root->val;
        if (value <= l || value >= r) return false;
        return checkBST(root->left, l, value) && checkBST(root->right, value, r);
    }
};
```









### [230. 二叉搜索树中第K小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/)



#### 3/4第一次做，精巧的中序遍历，并且时间复杂度是O(k)

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        // 中序遍历
        stack<TreeNode *> stack;
        while (root != nullptr || stack.size() > 0) {
            while (root != nullptr) {
                stack.push(root);
                root = root->left;
            }
            root = stack.top();
            stack.pop();
            --k;
            if (k == 0) break;
            root = root->right;
        }
        return root->val;


    }
};
```



#### 3/4第一次做也是中序遍历，acwing写法

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int k, ans;
    int kthSmallest(TreeNode* root, int _k) {
        k = _k;
        dfs(root);
        return ans;
    }
    void dfs(TreeNode* root) {
        if (!root) return;
        dfs(root->left);
        if (k == 0) return;
        if (--k == 0) {
            ans = root->val;
            return;
        }
        dfs(root->right);
    }
};
```



#### 3/4记录子树节点数的做法，需要记得能说思路

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

class MyBst {
public:
    MyBst(TreeNode *root) {
        this->root = root;
        countNodeNum(root);
    }
    int kthSmallest(int k) {
        TreeNode *node = root;
        while (node != nullptr) {
            int left = getNodeNum(node->left);
            if (left < k - 1) {
                node = node->right;
                k -= left + 1;
            } else if (left == k - 1) {
                break;
            } else {
                node = node->left;
            }
        }
        return node->val;
    }
private:
    TreeNode* root;
    unordered_map<TreeNode *, int> nodeNum;
    int countNodeNum(TreeNode *node) {
        if (node == nullptr) {
            return 0;
        }
        nodeNum[node] = 1 + countNodeNum(node->left) + countNodeNum(node->right);
        return nodeNum[node];
    }
    int getNodeNum(TreeNode* node) {
        if (node != nullptr && nodeNum.count(node)) {
            return nodeNum[node];
        }
        else return 0;
    }
};

class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        MyBst bst(root);
        return bst.kthSmallest(k);
    }
};
```





#### 3/4第一次做，中序遍历的做法，不够精巧

```cpp
    /**
    * Definition for a binary tree node.
    * struct TreeNode {
    *     int val;
    *     TreeNode *left;
    *     TreeNode *right;
    *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
    *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
    * };
    */
    class Solution {
    public:
        // 想要找出某个第k小的数字，就要用到二叉搜索树中序遍历为递增数列的性质
        vector<int> res;
        int kthSmallest(TreeNode* root, int k) {
            inorderTraverse(root);
            return res[k - 1];
        }
        void inorderTraverse(TreeNode* root) {
            if (!root) return;
            inorderTraverse(root->left);
            res.push_back(root->val);
            inorderTraverse(root->right);
        }
    };
```









#### 原答案

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* pre = NULL;
    bool isValidBST(TreeNode* root) {
        if (root == NULL) return true;
        bool left = isValidBST(root->left);
        if (pre && pre->val >= root->val) return false;
        pre = root;
        bool right = isValidBST(root->right);
        return left && right;
    }
};
```





### [199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)



#### 3/5第一次做，灵茶山艾府做法，实际上是从右侧开始的深度优先遍历

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> ans;
    void find(TreeNode* root, int d) {
        if (!root) return;
        if (d == ans.size()) ans.push_back(root->val);
        find(root->right, d + 1);
        find(root->left, d + 1);
    }
    vector<int> rightSideView(TreeNode* root) {
        // 需要发现每层只会有一个
        // 所以深度depth和ans.size()的大小是一致的
        // 而我们需要记录的是每一层最右边的那个值
        // 所以要先递归右子树，遍历完右子树再考虑左子树
        find(root, 0);
        return ans;
    }
};
```



#### 3/5第一次做 用的层序遍历，时间上会复杂一些，实际上是广度优先遍历

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        // 并不是一路root->right
        // 使用层序遍历的最后一个
        // 层序遍历使用queue
        if (!root) return {};
        vector<int> ans;
        queue<TreeNode*> visited;
        visited.push(root);
        while (!visited.empty()) {
            int n = visited.size();
            while (n--) {
                TreeNode* node = visited.front();
                if (n == 0) ans.push_back(node->val);
                visited.pop();
                if (node->left) visited.push(node->left);
                if (node->right) visited.push(node->right);
            }
        }
        return ans;
    }
};
```







#### 原答案

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    vector<int> ans;
    void find(TreeNode *root, int d) {
        if (root == nullptr) return;
        if (d == ans.size()) ans.push_back(root->val);
        find(root->right, d + 1);
        find(root->left, d + 1);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        find(root, 0);
        return ans;
    }
};
```





### [114. 二叉树展开为链表](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/)

前序遍历用vector和stack也能做



#### 3/5第一次做，找规律，很开心能做出这么优雅的方法

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        // 仔细观察就能发现，实际上这个先序遍历就是将所有的左子树都插到root和右子树之间
        if (!root) return;
        TreeNode* curr = root;
        while (curr) {
            if (curr->left) {
                TreeNode* next = curr->right;
                TreeNode* tmp = curr->left;
                while (tmp->right) {
                    tmp = tmp->right;
                }
                curr->right = curr->left;
                tmp->right = next;
                // 千万注意在将curr的左子树移到右边后，将左子树要设置成nullptr
                // 不然左右子树都是一模一样的
                curr->left = nullptr;
            }
            curr = curr->right;
        }
    }
};
```





### [105. 从前序与中序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

注意数组中装的没有nullptr，也就是说前序遍历如果是{3, 9, 20}，那么我们是不知道9和20是在3的左边还是右边的

根节点一定是前序遍历的第一个点

找一个数的位置可以用哈希表来做

根据中序遍历根节点左边的长度在前序遍历中数一样长的数段，就是左子树

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<int, int> hash;
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = inorder.size();
        for (int i = 0; i < n; i++) hash[inorder[i]] = i;
        return build(preorder, inorder, 0, preorder.size() - 1, 0, inorder.size() - 1);
    }
    TreeNode* build(vector<int>& preorder, vector<int>& inorder, int pl, int pr, int il, int ir) {
        if (pl > pr) return nullptr;
        TreeNode* root = new TreeNode(preorder[pl]);
        int k = hash[root->val];
        // 通过前序遍历确定下一个根节点
        // 通过中序遍历确定根节点的左右儿子
        root->left = build(preorder, inorder, pl + 1, pl + 1 + k - 1 - il, il, k - 1);
        root->right = build(preorder, inorder, pl + 1 + k - 1 - il + 1, pr, k + 1, ir);
        return root;
    }
};
```







### [437. 路径总和 III](https://leetcode.cn/problems/path-sum-iii/)



求一个区间内是否有连续的数段的和为一个特定值：使用前缀和

用哈希表存一下前面出现过的前缀和就行了



#### 前缀和例题

[560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        // 存的是各个前缀和出现的次数
        unordered_map<int, int> hash;
        hash[0] = 1;
        int sum = 0;
        int ans = 0;
        for (int i = 0; i < nums.size(); i++) {
            // cout << "i" << i << "sum" << sum << endl;
            sum += nums[i];
            ans += hash[sum - k];
            hash[sum]++;
        }
        return ans;
    }
};
```



#### 3/8  第一次做

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<long long, int> hash;
    int ans = 0;
    int pathSum(TreeNode* root, int targetSum) {
        // 看描述感觉是dfs
        // 要维护一个全局的哈希表，只要在一路向下，在返回的时候删去这个节点的和的次数即可
        // 路径方向向下即可，也就是可以转折，就是先向左再向右
        hash[0] = 1;
        dfs(root, targetSum, 0);
        return ans;
    }
    void dfs(TreeNode* root, long long sum, long long curr) {
        if (!root) return;
        curr += root->val;
        ans += hash[curr - sum];
        hash[curr]++;
        dfs(root->left, sum, curr), dfs(root->right, sum, curr);
        hash[curr]--;
    }
};
```









### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)



#### 3/8 复习

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 一共只有三种情况
        // 1. 在root的左右子树中
        // 2. p为root
        // 3. q为root

        // 情况2和情况3，第一行代码就解决了
        if (root == p || root == q || root == nullptr) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left && right) return root;
        if (left) return left;
        if (right) return right;
        return nullptr;
    }
};
```





#### 原答案

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 假设节点是p，如果q在p的子树中，那么直接返回p
        // 如果q不在p的子树中，还是需要返回q，使得上面的节点能够同时收到p和q
        if (root == p || root == q || root == NULL) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left && right) return root;
        if (left) return left;
        if (right) return right;
        return NULL;
    }
};
```



### [124. 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/)



#### 3/8acwing做法，更加简洁

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int ans;
    int maxPathSum(TreeNode* root) {
        ans = INT_MIN;
        dfs(root);
        return ans;
    }
    // 每次向上传递的都是经过这个点的最大值
    int dfs(TreeNode* root) {
        if (!root) return 0;
        int left = max(0, dfs(root->left));
        int right = max(0, dfs(root->right));
        // 每个节点最多只能连接两条边
        // 1. 不再向上传递，两条边连接左右子树
        ans = max(ans, left + right + root->val);
        // 2. 继续向上传递，一条边向上连接，另外一条边连接大的子树
        return root->val + max(left, right);
    }
};
```





#### 3/8第一次自己尝试，成功做出，可以更简洁

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int ans = INT_MIN;
    int maxPathSum(TreeNode* root) {
        maxPathSumImpl( root);
        return ans;
    }
    int maxPathSumImpl(TreeNode* root) {
        if (!root) return INT_MIN;
        int left = maxPathSumImpl(root->left);
        int right = maxPathSumImpl(root->right);
        int k = max(left, right);
        
        // 每个节点最多只能连接两条边
        // 1. 不再向上传递，两条边连接左右子树
        if (left > 0 && right > 0) ans = max(ans, left + right + root->val);

        // 2. 继续向上传递，一条边向上连接，另外一条边连接大的子树
        if (k > 0) {
            int n = root->val + k;
            ans = max(n, ans);
            return n;
        }
        else {
            ans = max(root->val, ans);
            return root->val;
        }
    }
};
```





## 图论

bfs记得使用队列

### [200. Number of Islands](https://leetcode.cn/problems/number-of-islands/)

dfs是看一下上下左右四个格子如果，某个格子没有走过的话，那么就会递归继续搜，直到把所有相连通的1找出来为止

如果说是bfs的话，就是将上下左右四个各自没有扩展过的格子放在队列里面



#### 3/10第一次做，dfs做法

```cpp
class Solution {
public:
    // flood-fill算法：bfs和dfs都可以解决
    // dfs比bfs方便的地方在于可以不用写队列
    int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0, -1, 0};
    int numIslands(vector<vector<char>>& grid) {
        int ans = 0;
        int m = grid.size(), n = grid[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1' && visited[i][j] == false) {
                    ans++;
                    dfs(grid, visited, i, j);
                }
            }
        }
        return ans;
    }
    void dfs(vector<vector<char>>& grid, vector<vector<bool>>& visited, int a, int b) {
        visited[a][b] = true;
        for (int i = 0; i < 4; i++) {
            int x = a + dx[i], y = b + dy[i];
            if (x < 0 || x >= grid.size() || y < 0 || y >= grid[a].size()) continue;
            if (grid[x][y] == '1' && visited[x][y] == false) {
                dfs(grid, visited, x, y);
            }
        }
    }
};
```





#### 3/10第一次做，bfs做法

```cpp
class Solution {
public:
    int number = 0;
    int dx[4] = {0, 1, 0, -1};
    int dy[4] = {1, 0, -1, 0};
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1' && visited[i][j] == false) {
                    number++;
                    bfs(grid, i, j, visited);
                }
            }
        }
        return number;
    }
    void bfs(vector<vector<char>>& grid, int i, int j, vector<vector<bool>>& visited) {
        queue<pair<int, int>> q;
        q.push(make_pair(i, j));
        visited[i][j] = true;
        
        while (!q.empty()) {
            pair<int, int> p = q.front();
            int a = p.first;
            int b = p.second;
            q.pop();
            for (int i = 0; i < 4; i++) {
                int nx = a + dx[i], ny = b + dy[i];
                if (nx < 0 || nx >= grid.size() || ny < 0 || ny >= grid[0].size()) continue;
                if (grid[nx][ny] == '1' && visited[nx][ny] == false) {
                    q.push(make_pair(nx, ny));
                    visited[nx][ny] = true;
                }
            }
        }
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    int dx[4] = {0, 1, 0, -1}, dy[4] = {-1, 0, 1, 0};
    void bfs(vector<vector<char>> & grid, vector<vector<bool>> & visited, int x, int y) {
        queue<pair<int, int>> que;
        que.push({x, y});
        visited[x][y] = true;
        while (!que.empty()) {
            pair<int, int> cur = que.front();
            que.pop();
            int a = cur.first;
            int b = cur.second;
            for (int i = 0; i < 4; i++) {
                int netx = a + dx[i];
                int nety = b + dy[i];
                if (netx < 0 || nety < 0 || netx >= grid.size() || nety >= grid[0].size()) continue;
                if (!visited[netx][nety] && grid[netx][nety] == '1') {
                    que.push({netx, nety});
                    visited[netx][nety] = true;
                }
            }
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int n = grid.size(), m = grid[0].size();
        vector<vector<bool>> visited = vector<vector<bool>>(n, vector<bool>(m, false));
        int result = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (!visited[i][j] && grid[i][j] == '1') {
                    result++;
                    bfs(grid, visited, i, j);
                }
            }
        }
        return result;
    }
};
```





### [994. 腐烂的橘子](https://leetcode.cn/problems/rotting-oranges/)

#### 3/10第一次做比较简单的bfs做法，限制的条件有些多，要想清楚

```cpp
class Solution {
public:
    int dx[4] = {0, 1, 0, -1}, dy[4] = {-1, 0, 1, 0};
    int orangesRotting(vector<vector<int>>& grid) {
        int ans = -1;
        // 用来记录新鲜橘子的数量
        int newOrange = 0;
        int m = grid.size(), n = grid[0].size();
        // 毫无疑问，使用bfs算法
        queue<pair<int, int>> visited;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) visited.push(make_pair(i, j));
                if (grid[i][j] == 1) newOrange++;
            }
        }
        // 如果没有新鲜橘子，直接返回
        if (newOrange == 0) return 0;
        // 如果没有那就直接返回
        // 如果有腐烂的橘子，每分钟bfs一圈
        while (!visited.empty()) {
            ans++;
            int size = visited.size();
            for (int i = 0; i < size; i++) {
                pair<int, int> p = visited.front();
                int a = p.first, b = p.second;
                visited.pop();
                // grid[a][b] = 2;
                for (int j = 0; j < 4; j++) {
                    int x = a + dx[j], y = b + dy[j];
                    if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size()) continue;
                    if (grid[x][y] == 1) {
                        newOrange--;
                        grid[x][y] = 2;
                        visited.push(make_pair(x, y));
                    } 
                }
            }
        }
        // 如果还有新鲜橘子没有腐烂，说明是一座孤岛，不可能被腐烂到了
        if (newOrange > 0) return -1;
        return ans;
    }
};
```







### [207. 课程表](https://leetcode.cn/problems/course-schedule/)



这是一道有向图求拓扑排序的问题：图的bfs的应用

或者说这个求这个有向图中是否有环

有向图才有拓扑序列：对于一个图中，对于每条有向边xy，x永远在y前面，那么就是一个拓扑序列

不是所有图都有拓扑序，但是有向无环图必定有拓扑序列 

一个有向无环图一定至少存在一个入度为0的点（证明：抽屉原理）



入度：指向自己的边数；出度：指向别人的边数

所有入度为0的都能排在前面指向别人

将所有入度为0的点入队，然后当队列不是空的时候，将所有的出边删掉，只影响j的入度减一





1.  统计所有点的入度，就是有多少条边指向它
2. 将所有入度为0的点加入队列，队列维护的就是所有当前入度为0的点
3. 然后从入度为0的点出发，向外扩散，每到一个点，它的入度就减一，如果刚好他的入度减为0，那么也加入队列
4. 最后判断是不是所有点都已经被遍历过了

#### 3/10非常模板非常经典的一道拓扑排序问题，多做几遍！

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        // 拓扑排序问题的特殊解法:是图的bfs应用
        // 记录每个点的入度
        vector<int> d(numCourses);
        // 对于[x, y],必须要先学过y才能学习x
        // g中记录的是每个点的出边，这样当a的入度 == 0的时候，我们就能将g[a]中所有的出边给删除
        vector<vector<int>> g(numCourses);
        for (auto& p : prerequisites) {
            int a = p[0], b = p[1];
            d[a]++;
            g[b].push_back(a);
        }

        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (d[i] == 0) q.push(i);
        }
        int count = 0;
        while (!q.empty()) {
            count++;
            int x = q.front();
            q.pop();
            for (int i = 0; i < g[x].size(); i++) {
                if (--d[g[x][i]] == 0) {
                    q.push(g[x][i]);
                }
            }
        }
        return count == numCourses;
    }
};
```





### [208. 实现 Trie (前缀树)](https://leetcode.cn/problems/implement-trie-prefix-tree/)

在 C++ 中，`this` 关键字是一个指针，指向对象本身的内存地址

#### 3/10第一次做，非常经典值得做很多次，总是忘记

```cpp
class Trie {
    vector<Trie*> children;
    bool isEnd;
    Trie* searchPrefix (string word) {
        Trie* node = this;
        for (char ch : word) {
            ch = ch - 'a';
            if (node->children[ch] == nullptr) {
                return nullptr;
            }
            else {
                node = node->children[ch];

            }
        }
        return node;
    }

public:
    Trie() : children(26), isEnd(false) {}
    
    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            ch = ch - 'a';
            if (node->children[ch] == nullptr) {
                node->children[ch] = new Trie();
                node = node->children[ch];
            }
            else node = node->children[ch];
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        Trie* node = searchPrefix(word);
        return node != nullptr && node->isEnd == true;
    }
    
    bool startsWith(string prefix) {
        Trie* node = searchPrefix(prefix);
        return node != nullptr;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```





#### 原答案

```cpp
class Trie {
private:
    vector<Trie*> children;
    bool isEnd;
    Trie* searchPrefix(string word) {
        Trie* node = this;
        for (char ch : word) {
            ch -= 'a';
            if (node->children[ch] == nullptr) {
                return nullptr;
            }
            node = node->children[ch];
        }
        return node;
    }

public:
    Trie() : children(26), isEnd(false) {}
    
    void insert(string word) {
        Trie* node = this;
        for (char ch : word) {
            ch -= 'a';
            if (node->children[ch] == nullptr) {
                node->children[ch] = new Trie();
            }
            node = node->children[ch];
        
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        Trie* node = searchPrefix(word);
        return node != nullptr && node->isEnd == true;
    }
    
    bool startsWith(string prefix) {
        Trie* node = searchPrefix(prefix);
        return node != nullptr;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```





## 回溯

### [46. 全排列](https://leetcode.cn/problems/permutations/)

#### 3/11第一次做用swap，感觉更加优雅一些

```cpp
class Solution {
public:
    // 第二种方法用来保证不会再dfs已经经过的点：
    // 既然数组中的数字是定的，我们只需要每次dfs将我们想要的那个数字swap过来就行了
    vector<vector<int>> ans;
    vector<vector<int>> permute(vector<int>& nums) {
        dfs(nums, 0);
        return ans;
    }
    void dfs(vector<int>& nums, int n) {
        // n：正在确定nums的第几个位置
        if (n == nums.size()) ans.push_back(nums);
        for (int i = n; i < nums.size(); i++) {
            // n之前的位置都已经确定好了，不能动
            swap(nums[i], nums[n]);
            dfs(nums, n + 1);
            // 注意nums是动态维护的数组
            // 不要忘记撤销掉动态维护的数组
            swap(nums[i], nums[n]);
        }
    }
};
```



#### 3/11第一次做，第一种实现方式

```cpp
class Solution {
public:
    // 两种方法来保证我们不会再dfs已经经过的点
    // 第一种是通过一个全局的vector<bool> visited数组来确保没有重复访问
    // 第二种巧妙的办法是在dfs第n位数时，将dfs到的那个数换到第n位上来，那么从0~n-1就是path
    vector<bool> visited;
    vector<vector<int>> ans;
    vector<vector<int>> permute(vector<int>& nums) {
        int n = nums.size();
        visited = vector<bool>(n, false);
        vector<int> path;
        dfs(nums, path, 0);
        return ans;
    }
    void dfs(vector<int>& nums, vector<int>& path, int n) {
        if (n == nums.size()) ans.push_back(path);
        for (int i = 0; i < nums.size(); i++) {
            if (visited[i] == false) {
                path.push_back(nums[i]);
                visited[i] = true;
                dfs(nums, path, n+1);
                visited[i] = false;
                path.pop_back();
            }
        }
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> path(nums.size());
        vector<bool> mark(nums.size(), false);
        function<void(int)> dfs = [&] (int i) {
            if (i == nums.size()) {
                ans.emplace_back(path);
                return;
            }
            for (int j = 0; j < nums.size(); j++) {
                if (mark[j] == false) {
                    path[i] = nums[j];
                    mark[j] = true;
                    dfs(i + 1);
                    mark[j] = false;
                }
            }
        };
        dfs(0);
        return ans;
    }
};
```







### [78. 子集](https://leetcode.cn/problems/subsets/)

#### 3/11第一次做，不难，但是不要忘记return

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> subsets(vector<int>& nums) {
        // 注意这道题不需要有顺序
        vector<int> path;
        dfs(nums, 0, path);
        return ans;
    }
    void dfs(vector<int>& nums, int n, vector<int>& path) {
        if (n == nums.size()) {
            ans.push_back(path);
            // 千万不要忘记这个return!
            return;
        }
        // 不要第n位上的数字
        dfs(nums, n + 1, path);
        // 要第n位上的数字
        path.push_back(nums[n]);
        dfs(nums, n + 1, path);
        path.pop_back();
    }
};
```







### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

#### 3/11第一次做，输入矩阵的时候不要忘记打逗号

```cpp
class Solution {
public:
    // 千万注意这个而矩阵不要输错，漏打逗号！
    vector<string> tel = {"", "", "abc", "def",
                        "ghi", "jkl", "mno",
                        "pqrs", "tuv", "wxyz"};
    vector<string> ans;
    vector<string> letterCombinations(string digits) {
        string path;
        dfs(digits, path, 0);
        return ans;
    }
    void dfs(string& digits, string& path, int n) {
        if (n == digits.size()) {
            if (path.size() != 0) ans.push_back(path);
            return;
        }
        
        for (int i = 0; i < tel[digits[n] - '0'].size(); i++) {
            path += tel[digits[n] - '0'][i];
            dfs(digits, path, n+1);
            path.pop_back();
        }
    }
};
```





#### 原答案

```cpp
class Solution {
    string map[10] = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
public:
    vector<string> letterCombinations(string digits) {
        int n = digits.length();
        if (n == 0) return {};
        vector<string> ans;
        // 初始化n个字符，然后初始化所有字母为0
        string path(n, 0);
        // function<void(int)>表示是一个函数模板
        // 返回的是void 输入的是int
        // [&]表示函数内能够调用所有外部变量的引用
        // int i 表示输入的变量是i
        function<void(int)> dfs = [&] (int i) {
            if (i == n) {
                ans.emplace_back(path);
                return;
            }
            for (char c : map[digits[i] - '0']) {
                path[i] = c;
                dfs(i + 1);
            }
        };
        dfs(0);
        return ans;
    }
};
```









### [39. 组合总和](https://leetcode.cn/problems/combination-sum/)

#### 3/11acwing写法非常简洁，值得学习

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> path;
        dfs(candidates, path, target, 0);
        return ans;
    }
    void dfs(vector<int>& candidates, vector<int>& path, int target, int n) {
        if (target == 0) {
            ans.push_back(path);
            return;
        }
        if (n == candidates.size()) return;
        for (int i = 0; candidates[n] * i <= target; i++) {
            // 先进行dfs，因为需要有i = 0的情况
            dfs(candidates, path, target - candidates[n] * i, n + 1);
            path.push_back(candidates[n]);
        }
        for (int i = 0; candidates[n] * i <= target; i++) {
            path.pop_back();
        }
    }
};
```





### 3/11第一次做，不简洁，但是剪枝得好

因为是所有方案，所以很难有什么优化，直接暴搜就行

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        // 典型的组合求和问题，是使用回溯来做的，而且更加容易实现剪枝
        vector<int> path;
        dfs(candidates, path, 0, 0, target);
        return ans;
    }
    void dfs(vector<int>& candidates, vector<int>& path, int n, int sum, int target) {
        if (n == candidates.size() - 1) {
            if ((target - sum) % candidates[n] == 0) {
                int m = (target - sum) / candidates[n];
                int m2 = m;
                // cout << m << endl;
                while (m--) path.push_back(candidates[n]);
                ans.push_back(path);
                while (m2--) path.pop_back();
                return;
            }
            else return;
        }
        
        int m = (target - sum) / candidates[n];
        for (int i = 0; i <= m; i++) {
            int x1 = i, x2 = i;
            while (x1--) {
                path.push_back(candidates[n]);
                sum += candidates[n];
            }
            dfs(candidates, path, n + 1, sum, target);
            while(x2--) {
                path.pop_back();
                sum -= candidates[n];
            }
        }
    }


};
```





### [22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)



#### 3/11第一次做，还是比较简单的思考

```cpp
class Solution {
public:
    // 很明显1. 要给出所有的排列组合，那么暴搜无法避免；2. 这道题的性质是任何时候右括号的数量要小于等于左括号的数量 
    // 3.那么就是还需要添加的右括号的数量要大于左括号的数量
    vector<string> ans;
    vector<string> generateParenthesis(int n) {
        string path;
        dfs(path, n, n);
        return ans;
    }
    void dfs(string& path, int left, int right) {
        if (left == 0) {
            int x = right;
            while (x--) path += ')';
            ans.push_back(path);
            while (right--) path.pop_back();
            return;
        }
        // 对于每一次dfs要么加左括号
        path += '(';
        dfs(path, left - 1, right);
        path.pop_back();
        // 要么加右括号
        if (right > left) {
            path += ')';
            dfs(path, left, right - 1);
            path.pop_back();
        }
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string path;
        function<void(int, int)> dfs = [&] (int l, int r) {
            if (l == 0 && r == 0) {
                ans.emplace_back(path);
                return;
            }
            if (r > l) {
                path.push_back(')');
                dfs(l, r - 1);
                path.pop_back();
            }
            if (l > 0) {
                path.push_back('(');
                dfs(l - 1, r);
                path.pop_back();
            }
        };
        dfs(n, n);
        return ans;
    }
};
```





### [79. 单词搜索](https://leetcode.cn/problems/word-search/)



#### 3/11 第一次做，自己的dfs方法，但是能做出来

```cpp
class Solution {
public:
    int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0, -1, 0};
    bool exist(vector<vector<char>>& board, string word) {
        // 需要找出所有的可能情况，使用暴搜
        int m = board.size(), n = board[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word[0]) {
                    if (dfs(board, visited, word, i, j, 1)) {
                        return true;
                    }
                }
            }
        }
        return false;
    }
    bool dfs(vector<vector<char>>& board, vector<vector<bool>>& visited, string& word, int a, int b, int n) {
        if (n == word.size()) return true;
        visited[a][b] = true;
        for (int i = 0; i < 4; i++) {
            int x = a + dx[i], y = b + dy[i];
            if (x < 0 || y < 0 || x >= board.size() || y >= board[0].size()) continue;
            if (board[x][y] == word[n] && visited[x][y] == false) {
                if (dfs(board, visited, word, x, y, n + 1)){
                    return true;
                }
            }
        }
        visited[a][b] = false;
        return false;
    }
};
```





### [131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)

#### 3/11第一次做，不要思考的太过复杂，对于回文串的处理以及dfs的情况处理，建议多做几遍

```cpp
class Solution {
public:
    // 1. 判断是否为回文串
    // 2. dfs分割暴搜

    // 注意检查回文一般回直接通过字符串的索引来进行，而不需要额外的结构
    vector<vector<string>> ans;
    vector<vector<string>> partition(string s) {
        vector<string> path;
        dfs(s, 0, path);
        return ans;
    }

    void dfs(string& s, int start, vector<string>& path) {
        if (start == s.size()) {
            ans.push_back(path);
            return;
        }
        for (int end = start; end < s.size(); end++) {
            if (isPalindrome(s, start, end)) {
                path.push_back(s.substr(start, end - start + 1));
                dfs(s, end + 1, path);
                path.pop_back();
            }

        }
    }

    bool isPalindrome(string& s, int start, int end) {
        while (start < end) {
            if (s[start++] != s[end--]) {
                return false;
            }
        }
        return true;
    }
};
```







### [51. N 皇后](https://leetcode.cn/problems/n-queens/)



#### 3/11第一次做，N皇后问题的思考值得多做几次

```cpp
class Solution {
public:
    // 第一点每一行只能放一个
    // 如何存储已经被占领的列

    // 同一个斜边应该如何表示:(i, j)
    // 左上右下：j = i -> j - i + n 取值范围是0 - (n - 1) + n = 1 ~2n -1
    // 右上左下: j = -i-> j + i 取值范围是0~2n-2
    // 对角线的：diagonal
    
    vector<bool> dg;
    vector<bool> udg;
    vector<bool> col;
    vector<string> path;
    vector<vector<string>> ans;
    vector<vector<string>> solveNQueens(int n) {
        dg = vector<bool>(2 * n, false);
        udg = vector<bool> (2 * n, false);
        col = vector<bool>(n, false);
        path = vector<string>(n, string(n, '.'));
        dfs(0);
        return ans;
    }
    // i代表处理第i行放置的东西
    void dfs(int i) {
        int n = path.size();
        if (i == n) {
            ans.push_back(path);
            return;
        }
        for (int j = 0; j < path.size(); j++) {
            if (!col[j] && !dg[j + i] && !udg[j - i + n]) {
                path[i][j] = 'Q';
                col[j] = dg[j + i] = udg[j - i + n] = true;
                dfs(i + 1);
                path[i][j] = '.';
                col[j] = dg[j + i] = udg[j - i + n] = false;
            }
        }
    }
};
```







#### 原答案

```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        // 思考：如何只查询一次就能表示对角线上出现过Q
        // 左上右下如何对角线如何表示？

        // 以第0行，第2格上放Q为例 (i, j)
        // 左上右下： j - i + n (这里+n是因为j - i)
        // 右上左下 j + i

        vector<vector<string>> ans;
        vector<int> tmp;
        // 请一定不要忘记使用下面这种string数组的声明方法
        // vector<string> path(n, string(n, '.'));

        // vector<string> path;
        // for (int i = 0; i < n; i++ ) {
        //     for (int j =0;j < n ;j++) {
        //         path[i][j] ='.';
        //     }
        // }
        vector<string> path(n);
        for (int i = 0; i < n; i++) {
                path[i] = string(n, '.');
        }
        vector<bool> col(n, false), dg(2 * n, false), udg(2 * n, false);
        
        function<void(int)> dfs = [&] (int i) {
            if (i == n) {
                ans.emplace_back(path);
                return;
            }
            for (int j = 0; j < n; j++) {
                if (!col[j] && !dg[j + i] && !udg[j - i + n]) {
                    path[i][j] = 'Q';
                    col[j] = dg[j + i] = udg[j - i + n] = true;
                    dfs(i + 1);
                    col[j] = dg[j + i] = udg[j - i + n] = false;
                    path[i][j] = '.';
                }
            }
        };
        dfs(0);
        return ans;
    }
};
```







## 二分查找

### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

#### 3/19第一次做

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            int x = nums[mid];
            // 找大于等于target的最小值
            if (x < target) {
                l = mid + 1;
            }
            else {
                r = mid;
            }
        }
        if (nums[l] == target) return l;
        else if (l == nums.size() - 1 && target > nums[l]) return l + 1;
        return l;
    }
};
```



```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] >= target) r = mid;
            else l = mid + 1; 
        }
        printf("%d %d", l, r);
        if (nums[l] == target) return l;
        else if (l == nums.size() - 1 && target > nums[l]) return l + 1;
        else return l;
    }
};
```



### [74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/)

#### 3/19第一次做

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        int l = 0, r = m * n - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            int rm = mid / n;
            int rn = mid - (n * rm);
            // if (rm < 0 || rm >= m || rn < 0 || rn >= n) {
            //     cout << mid << ' ' << rm << ' ' << rn << endl;
            //     return false;
            // }
            int x = matrix[rm][rn];
            if (x < target) {
                l = mid + 1;
            }
            else r = mid;
        }
        int rm = l / n;
        int rn = l- (n * rm);
        if (matrix[rm][rn] == target) return true;
        else return false;

    }
};
```





### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

#### 3/19第一次做，二分真的不难

```cpp
class Solution {
public:
    int searchLeft(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            int x = nums[mid];
            if (x >= target) {
                r = mid;
            }
            else l = mid + 1;
        }
        return l;
    }

    int searchRight(vector<int>& nums, int target) {
        
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1)>> 1;
            int x = nums[mid];
            if (x <= target) {
                l = mid;
            }
            else r = mid - 1;
        }
        return l;
    }

    vector<int> searchRange(vector<int>& nums, int target) {
        if (!nums.size()) return {-1, -1};
        // 需要找出大于等于t的最小值，以及小于等于t的最大值
        // 两次二分即可
        int l = searchLeft(nums, target);
        int r = searchRight(nums, target);
        if (nums[l] == target && nums[r] == target) return {l, r};
        else return {-1, -1};
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    int searchLeft(vector<int>& nums, int target) {
       int l = 0, r = nums.size() - 1;
       // 寻找左边界（即大于等于），对于r来说就是糊涂账，但是l非常清楚，就是当小于时，l必定需要+1
       while (l < r) {
           int mid = (l + r) >> 1;
           if (nums[mid] < target) l = mid + 1;
           else r = mid;
       }
       return l;
    }
    int searchRight(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            // 寻找右边界（小于等于），那么直接看大于的情况
            if (nums[mid] > target) r = mid - 1;
            else l = mid;
        }
        return l;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        if (!nums.size()) return {-1, -1};
        int l = searchLeft(nums, target);
        int r = searchRight(nums, target);
        if (nums[l] == target && nums[r] == target) return {l, r};
        else return {-1, -1};
    }
};
```





### [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

#### 3/19 第一次做脑子要清楚一点，有好多边界条件，建议重做

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // 如果要二分前半段的最高点就要和nums[0]比较，如果想二分后半段的最低点就要和nums[nums.size() - 1]比较
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            int x = nums[mid];
            if (x >= nums[0]) l = mid;
            else r = mid - 1;
        }
        if (target >= nums[0]) r = l, l = 0;
        else l = r + 1, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            int x = nums[mid];
            if (x >= target) r = mid;
            // 注意如果nums只有一个数的时候并且x< target，那么会导致l = 1, r  =0,l有出界的风险，所以return的时候需要return r
            else l = mid + 1;

        }
        cout << l << " " << r << endl;
        if (nums[r] == target) return r;
        else return -1; 


    }
};
```





#### 原答案

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            if (nums[mid] >= nums[0]) l = mid;
            else r = mid - 1;
        }
        if (target >= nums[0]) l = 0;
        else l = r + 1, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] >= target) r = mid;
            else l = mid + 1; // 这里l有出界的风险，所以return的时候需要return的是r，而不能是l
        }
        if (nums[r] == target) return r;
        else return -1;
    }
};
```





### [153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)



#### 3/19 第一次做很简单

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        // 所有整数互不相同，继续使用二分即可
        // 这次二分后半段的最小值吧
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            int x = nums[mid];
            if (x <= nums[nums.size() - 1]) r = mid;
            else l = mid + 1;
        }
        return nums[l];
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        // 直接分类讨论画图，主要就是三种情况，左边长，右边长，以及没有旋转
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] > nums[nums.size() - 1]) l = mid + 1;
            else r = mid;
        }
        return nums[l];
    }
};
```







#### 原答案

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
        int si = min((int)nums1.size(), (i + k / 2));
        int sj = j + k - k /2;
        // 这里指的是第几个，所以必须要 -1
        if (nums1[si - 1] > nums2[sj  - 1]) {
            return find(nums1, i, nums2, sj, k - (sj - j));
        } else return find(nums1, si, nums2, j, k - (si - i));
    } 
};
```







## 栈

### [20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> stk;
        for (int i = 0; i < s.size(); i++) {
            if (!stk.empty()) {
                char c = stk.top();
                if ((c == '{' && s[i] == '}') ||
                    (c == '[' && s[i] == ']') ||
                    (c == '(' && s[i] == ')')) {
                        stk.pop();
                    }
                    else stk.push(s[i]);
            }
            else stk.push(s[i]);
        }
        return stk.empty();
    }
};
```





#### 原答案

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> tmp;
        for (int i = 0; i < s.size(); i++) {
            char ch = s[i];
            if (!tmp.empty()) {
                char chStack = tmp.top();
                if ((ch == '}' && chStack == '{') ||
                (ch == ']' && chStack == '[') ||
                (ch == ')' && chStack == '(')) tmp.pop();
                else tmp.push(ch);
            }
            else {
                tmp.push(s[i]);
            }
        }
        return tmp.empty();
    }
};
```





### [155. 最小栈](https://leetcode.cn/problems/min-stack/)

#### 3/19第一次做有趣的最小栈，要读明白题意，耐心一点

```cpp
class MinStack {
public:
// 相当于去维护一个前缀最小值的栈
// 用手画一遍就能懂规律了
    stack<int> stk;
    stack<int> min_stk;
    MinStack() {
        min_stk.push(INT_MAX);
    }
    
    void push(int val) {
        stk.push(val);
        min_stk.push(min(min_stk.top(), val));
    }
    
    void pop() {
        int val = stk.top();
        stk.pop();
        min_stk.pop();
    }
    
    int top() {
        return stk.top();
    }
    
    int getMin() {
        return min_stk.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```











## 堆

### [215. Kth Largest Element in an Array](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

多种解法，三种解法都必须要掌握！建议多做

#### 3/9第一次做，快速选择算法模板题目，建议将三种解法多做几遍

```cpp
class Solution {
public:
    // 快速选择算法的时间复杂度是O(2n)
    int quick_select(vector<int>& nums, int l, int r, int k) {
        if (l == r) return nums[k];
        int x = nums[l + r >> 1];
        int i = l - 1, j = r + 1;
        while (i < j) {
            do i++; while(nums[i] > x);
            do j--; while (nums[j] < x);
            if (i < j) swap(nums[i], nums[j]);
        }
        // 是在原数组基础上的k所以可以直接使用k
        if (k <= j) return quick_select(nums, l, j, k);
        else return quick_select(nums, j + 1, r, k);
    }
    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size();
        return quick_select(nums, 0, n - 1, k - 1);
    }
};
```





#### 3/9 第一次做，大根堆做法，手写大根堆，建议多写几次

```cpp
class Solution {
public:
    void maxHeapify(vector<int>& nums, int i, int heapsize) {
        int largest = i;
        // 注意是2*i+1和2*i+2
        int left = 2 * i + 1, right = 2 * i + 2;
        if (left < heapsize && nums[left] > nums[largest]) {
            largest = left;
        }
        // 注意这里仍然是if，不是else if！
        if (right < heapsize && nums[right] > nums[largest]) {
            largest = right;
        }
        if (i != largest) {
            swap(nums[i], nums[largest]);
            maxHeapify(nums, largest, heapsize);
        }
    }
    void buildMaxHeap(vector<int>& nums, int heapsize) {
        // 从最后一个非叶子节点向前不断向下down来维护堆
        for (int i = heapsize; i >= 0; i--) maxHeapify(nums, i, heapsize);
    }
    int findKthLargest(vector<int>& nums, int k) {
        // 如果使用大根堆
        // 那么将所有元素插入大根堆，然后将最大的k-1个元素弹出，那么堆顶就是第k大的元素
        
        // 需要手写大根堆
        int heapsize = nums.size();
        buildMaxHeap(nums, heapsize);
        // 如何弹出k - 1个元素？
        // 将最后一个元素覆盖到大根堆的顶部，然后down它
        for (int i = 0; i < k - 1; i++) {
            swap(nums[0], nums[heapsize - 1]);
            heapsize--;
            maxHeapify(nums, 0, heapsize);
        }
        return nums[0];
    }
};
```



#### 3/9第一次做小根堆stl做法

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        // 使用小根堆可以做
        // 可以用来联系小根堆的stl写法，C++默认的priority_queue是大根堆
        
        // 小根堆的思路是维护一个由最大的k个元素组成的堆，那么堆顶的元素就是我们的答案
        // 所以在不断插入的时候，如果出现比堆顶元素大的数，就要把堆顶元素弹出，然后插入这个数
        // 而如果插入的数比堆顶的元素要小，那么就不用做任何操作
        
        // 时间复杂度是nlongk, 空间复杂度是k

        priority_queue<int, vector<int>, greater<int>> min_heap;
        for (int  i = 0; i < nums.size(); i++) {
            if (min_heap.size() < k) {
                min_heap.push(nums[i]);
            }
            else if (nums[i] > min_heap.top()) {
                min_heap.pop();
                min_heap.push(nums[i]);
            }
        }
        return min_heap.top();
    }
};
```





#### [347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)

#### 3/19 使用大根堆做，正规的做法，时间复杂度是nlogk

```cpp
class Solution {
public:
    static bool cmp(pair<int, int>& m, pair<int, int>& n) {
        return m.second > n.second;
    }
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> hash;
        for (auto a : nums) {
            hash[a]++;
        }
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(&cmp)> q(cmp);
        for (auto [x, c] : hash) {
            q.push(make_pair(x, c));
            if (q.size() > k) {
                q.pop();
            }
        }
        vector<int> res;
        while (!q.empty()) {
            res.push_back(q.top().first);
            q.pop();
        }
        return res;


    }
};
```





#### 3/19第一次做计数排序做法，有点小幽默

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> hash;
        for (auto a : nums) hash[a]++;
        int n = nums.size();
        vector<int> s(n + 1);
        for (auto [x, c] : hash) s[c]++;
        int i = n, sum = 0;
        while (sum < k) {
            sum += s[i];
            i--;
        }
        vector<int> ans;
        for (auto [x, c] : hash) {
            if (c > i) ans.push_back(x);
        }
        return ans;
    }
};
```







## 贪心算法









## 动态规划

### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

#### 3/22第一次做

```cpp
class Solution {
public:
    int climbStairs(int n) {
        // 怎么思考
        // f[n] 代表的是第n阶有多少种到达的方法
        vector<int> f(n + 1);
        
        // 两种情况下一个阶梯
        // 第一种是从下面一个阶梯上来，只走一格
        // 第二种是从下面两个阶梯上来，直走两格
        // f[n] = f[n - 1] + f[n - 2];
        f[0] = 1;
        f[1] = 1;
        for (int i = 2; i <= n; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        return f[n];

    }
};
```





```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2) return n;
        // f[i] = f[i - 1] + f[i - 2]
        // int f[n + 1];
        int f1 = 1;
        int f2 = 2;
        for (int i = 3; i <= n; i++) {
            int f3 = f2 + f1;
            f1 = f2;
            f2 = f3;
        }
        return f2;
    }
};
```



### [118. 杨辉三角](https://leetcode.cn/problems/pascals-triangle/)

#### 3/22第一次做，要看清题目！！！

```cpp
class Solution {
public:
    vector<vector<int>> generate(int n) {
        // 状态转移方程
        // f[n][m] = f[n - 1][m - 1] + f[n - 1][m]
        vector<vector<int>> f;
        for (int i = 0; i < n; i++) {
            f.push_back(vector<int>(i + 1));
        }
        f[0][0] = 1;
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i + 1; j++) {
                if (j - 1 >= 0 && j - 1 < (i - 1) + 1) {
                    f[i][j] += f[i - 1][j - 1];
                }
                if (j >= 0 && j < (i - 1) + 1) {
                    f[i][j] += f[i - 1][j];
                }
            }
        }
        return f;
    }
};
```







#### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

#### 3/22第一次做，注意注意状态转移方程一定要用i来写！！！！

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        // f[i] = max(f[i - 1], f[i - 2] + nums[i])
        // f[i + 2] = max(f[i + 1], f[i] + nums[i + 2]);
        // vector<int> f(nums.size() + 2);
        int f0 = 0, f1 = 0;
        for (int i = 0; i < nums.size(); i++) {
            // f[i + 2] = max(f[i + 1], f[i] + nums[i]);
            int new_f = max(f1, f0 + nums[i]);
            f0 = f1;
            f1 = new_f;
        }
        return f1;
    } 
};
```





#### 原答案

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        // f[i] = max(f[i - 1], f[i - 2] + nums[i])
        // f[i + 2] = max(f[i + 1], f[i] + nums[i + 2]);
        // vector<int> f(nums.size() + 2);
        int f0 = 0, f1 = 0;
        for (int i = 0; i < nums.size(); i++) {
            // f[i + 2] = max(f[i + 1], f[i] + nums[i]);
            int new_f = max(f1, f0 + nums[i]);
            f0 = f1;
            f1 = new_f;
        }
        return f1;
    } 
};
```







## 多维动态规划

## 技巧


### [136. 只出现一次的数字](https://leetcode.cn/problems/single-number/)

异或有交换律和结合律

异或（相当于相减）：所有相同的数互相异或就是0 

0^0 = 0

1^1 = 0

1^0 = 1

#### 3/6第一次做

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        // 出现两次这个条件应该怎么使用？
        // 而且只能使用常量的额外空间
        // hash表，然后每次都删除
        // 使用异或，所有相同的数互相配对得到0，0和任何数n异或得到的就是n
        int res = 0;
        for (int i = 0; i < nums.size(); i++) res ^= nums[i];
        return res;
    }
};
```





### [169. 多数元素](https://leetcode.cn/problems/majority-element/)

#### 3/6第一次做，使用排序，但不是最优解，重新写了一遍快排

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        // 既然出现次数会大于n/2次，那么对nums进行排序，在nums中第n/2的位置的数必然是频率最高的数
        quick_sort(nums, 0, nums.size() - 1);
        return nums[nums.size() / 2];
    }
    void quick_sort(vector<int>& nums, int l, int r) {
        if (l >= r) return;
        int x = nums[l + r >> 1];
        int i = l - 1, j = r + 1;
        while (i < j) {
            do i++; while (nums[i] < x);
            do j--; while (nums[j] > x);
            if (i < j) swap(nums[i], nums[j]);
        }
        // 一定只能使用j 和 j + 1！！！
        quick_sort(nums, l, j);
        quick_sort(nums, j + 1, r);
    }
};
```



#### 3/6 第一次做使用投票算法非常巧妙

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int ans, freq = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (freq == 0) {
                ans = nums[i];
                freq++;
            }
            else if (nums[i] != ans) {
                freq--;
            }
            else {
                freq++;
            }
        }
        return ans;
    }
};
```

