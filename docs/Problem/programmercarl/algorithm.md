# 代码随想录笔记

## 1. 二分查找

二分查找的数学理解是单调函数的有解问题

注意点：

1. 在C++中STL的容器和算法中用的都是左闭右开区间，所以尽量使用左闭右开的区间来写二分查找

2. 在刷题时思考如果最后区间只剩下一个数或者两个数，自己的写 法是否会陷入死循环，如果某种写法无法跳出死循环，则考虑尝试另一种写法。

### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

```cpp
class Solution {
public:
    int searchLeft(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        return l;
    }
    int searchRight(vector<int>&nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            if (nums[mid] > target) r = mid - 1;
            else l = mid;
        }
        return l;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.size() == 0) return vector<int>{-1, -1};
        // 分别写两个function来搜索左边界和右边界
        int left = searchLeft(nums, target);
        int right = searchRight(nums, target);
        if (nums[left] == target && nums[right] == target) return vector<int>{left, right};
        else return vector<int>{-1, -1};
    }
};
```

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

# 灵茶山艾府课程

## 相向双指针

acwing的思路是引入j -1这个巧妙的技巧来不断控制右指针的移动

而灵茶山艾府的做法是同时控制左右指针，由于数组有序，那么当和比target大的时候就移动右指针，和比target小的时候就移动左指针





### [167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

时间复杂度O(n)

空间复杂度O(1)





#### acwing做法

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        vector<int> res;
        for (int i = 0, j = numbers.size() - 1; i < j; i++) {
            while (j - 1 > i && numbers[i] + numbers[j - 1] >= target) j--;
            if (numbers[i] + numbers[j] == target) res.push_back(i + 1), res.push_back(j + 1); 
        }
        // if (!res.empty()) return {-1, -1};
        return res;
    }
};
```

#### 灵茶山艾府

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0;
        int r = numbers.size() - 1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum == target) return {l + 1, r + 1};
            else if (sum > target) r--;
            else l++;
        }
        return {l + 1, r + 1}; //这句话用不到
    }
};
```



### [15. 三数之和](https://leetcode.cn/problems/3sum/)

#### acwing

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 1; i++) {
            if (i && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1, k = nums.size() - 1; j < k; j++) {
                if (j >= i + 2 && nums[j] == nums[j - 1]) continue;
                while (k - 1 > j && nums[i] + nums[j] + nums[k - 1] >= 0) k--;
                if (nums[i] + nums[j] + nums[k] == 0) res.push_back({nums[i], nums[j], nums[k]});
            }
        }
        return res;
    }
}; 
```



#### 灵茶山艾府



```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 2; i++) {
            int l = i + 1, r = nums.size() - 1;
            if (i && nums[i - 1] == nums[i]) continue;
            while (l < r) {
                int s = nums[i] + nums[l] + nums[r];
                if (s == 0) {
                    res.push_back({nums[i], nums[l], nums[r]});
                    r--;
                    while (r < nums.size() - 1 && nums[r] == nums[r + 1]) r--;
                }
                else if (s > 0) r--;
                else l++;
            }
        }
        return res;
    }
};
```





## 相向双指针 

### [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

时间复杂度: On

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





### [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/)

需要观察到性质：每个格子上面接的水就是左右两边各自最大值的最小值减去这个格子的高度

#### 第一种做法是前后缀分解



```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        vector<int> pre(height.size());
        vector<int> suf(height.size());
        int res = 0;
        pre[0] = height[0];
        suf[height.size() - 1] =height[height.size() - 1];
        for (int i = 1; i < height.size(); i++) pre[i] = max(pre[i - 1], height[i]);
        for (int i = height.size() - 2; i >= 0; i --) suf[i] = max(suf[i + 1], height[i]);
        for (int i = 0; i < height.size(); i++) {
            res += min(pre[i], suf[i]) - height[i];
        }
        return res;
    }
}; 
```



#### 第二种做法是双指针

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int ans = 0;
        int l = 0, r = height.size() - 1;
        int lmax = height[0], rmax = height[height.size() - 1];
        while (l < r) {
            lmax = max(lmax, height[l]), rmax = max(rmax, height[r]);
            if (lmax <= rmax) {
                ans += lmax - height[l];
                l++;
            }
            else {
                ans += rmax - height[r];
                r--;
            }
        }
        return ans;
    }
};
```



### [209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

时间复杂度O(n)

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int i = 0, j = 0, ans = nums.size() + 1,  res = 0;
        while (j < nums.size()) {
            res += nums[j];
            while (res >= target) {
                ans = min(ans, j - i + 1);
                res -= nums[i];
                i++;
            }
            j++;
        }
        return (ans <= n) ? ans : 0;
    }
};
```



### [713. 乘积小于 K 的子数组](https://leetcode.cn/problems/subarray-product-less-than-k/)

```cpp
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        // 我们需要关注的是所有以右端点为终点的数组的最长的长度
        // 注意读题是严格小于
        if (k <= 1) return 0;
        int l = 0, r = 0;
        int prod = 1;
        int res = 0;
        while (r < nums.size()) {
            prod *= nums[r];
            while (prod >= k) {
                prod /= nums[l];
                l++;
            }
            res += r - l + 1;
            r++;
        }
        return res;
    }
};
```



### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

注意哈希表的初始值是0

并且可以用s.empty()来判断字符串是否为空

时间复杂度是O(n)

由于字符是ascii码，最多只有128个，那么就可以将空间复杂度看成O(128)

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.empty()) return 0;
        unordered_map<char, int> hash;
        int l = 0, r = 0;
        int res = 1;
        while (r < s.size()) {
            hash[s[r]]++;
            while (hash[s[r]] > 1) {
                hash[s[l]]--;
                l++;
            }
            res = max(res, r - l + 1);
            r++;
        }
        return res;
    }
};
```



## 二分查找

### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res;
        // 注意判空！不然找问题非常浪费时间！
        if (nums.size() == 0) return {-1, -1};
        int l = 0, r = nums.size() - 1;
        //先找左端点
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        if (nums[l] == target) res.push_back(l);
        else return {-1, -1};
        // 找右端点
        l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r + 1) >> 1;
            if (nums[mid] > target) r = mid - 1;
            else l = mid; // l = mid 很危险
        }
        if (nums[l] == target) res.push_back(l);
        else return {-1, -1};

        return res;
    }
};
```

### [153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

有序数组旋转后做题的技巧是

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



### [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

#### 第一种做法是对着三个坐标点强行分类

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] <= nums[nums.size() - 1]) {
                if (target > nums[nums.size() - 1]) r = mid - 1;
                else if (target <= nums[nums.size() - 1] && target > nums[mid]) l = mid + 1;
                else r =  mid;
            } else {
                if (target <= nums[nums.size() - 1]) l = mid + 1;
                else if (target <= nums[mid]) r = mid;
                else l = mid + 1; 
            }
        }
        if (nums[l] == target) return l;
        else return -1;
    }
};
```



##### 第二种做法是先二分出旋转数组的分界点，然后再在特定的段上不断二分找出需要的数

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
};*
```





##  反转链表

### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

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
        if (head == NULL) return head;
        ListNode* a = head;
        ListNode* b = head->next;
        while (b != NULL) {
            ListNode* c = b->next;
            b->next = a;
            a = b;
            b = c;
        }
        head->next = NULL;
        return a;
    }
};
```



### [92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)

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
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (head == NULL || head->next == NULL) return head;
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* a = dummy;
        for (int i = 1; i < left; i++) a = a->next;
        ListNode* b = a->next;
        ListNode* c = b->next;
        for (int i = 0; i < right - left; i++) {
            ListNode* d = c->next;
            c->next = b;
            b = c;
            c = d;
        }
        a->next->next = c;
        a->next = b;
        return dummy->next;

    }
};
```





## 快慢指针

### [876. 链表的中间结点](https://leetcode.cn/problems/middle-of-the-linked-list/)

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
// 这道题很明显需要通过奇数和偶数分别分析
// 奇数情况简单：1,2,3 快指针+2，而慢指针+1，fast->next == NULL时停下
// 偶数情况：1, 2 这种情况仍然需要快指针+2，慢指针加1因为有两个中间节点的话，返回的时第二个中间节点
// 而偶数情况中快指针会指向NULL，这个时候就要停下 fast->next == NULL
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *fast = head;
        ListNode *slow = head;
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
        }
        return slow;
    }
};
```



### [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)

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







### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)



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
        // 入环前的长度时a，相遇时环内已经走过b，环内还剩下c
        // 快指针走过的路 a + k (b + c)
        // 慢指针走过的路 a + b
        // 2(a + b) = a + k(b + c)
        // a - c = (k - 1)(b + c)
        // 如果head和慢指针同时走a的路，那么head会到入环点，而慢指针会在转了(k - 1)圈之后到入环点
        ListNode *fast = head, * slow = head;
        while (true) {
            if (fast == NULL || fast->next == NULL) return NULL;
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) break;
        }
        ListNode *dummy = head;
        while (fast != dummy) {
            fast = fast->next;
            dummy = dummy->next;
        }
        return dummy;
    }
};
```



### [143. 重排链表](https://leetcode.cn/problems/reorder-list/)

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
    void reorderList(ListNode* head) {
        ListNode *fast = head, *slow = head;
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
        }
        fast = slow;
        slow = NULL;
        while (fast != NULL) {
            ListNode *temp = fast->next;
            fast->next = slow;
            slow = fast;
            fast = temp;
        }
        
        fast = head;
        
        while (fast->next != NULL && slow->next != NULL) {
            ListNode *l = fast->next;
            ListNode *r = slow->next;
            fast->next = slow;
            slow->next = l;
            fast = l;
            slow = r;
        }

    }
};
```







## 前后指针

### [237. 删除链表中的节点](https://leetcode.cn/problems/delete-node-in-a-linked-list/)

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
    void deleteNode(ListNode* node) {
        // 因为不是链表中的最后一个节点，而且只要保证所有值唯一即可
        // 那么将下一个值复制到这个节点，然后删去下一个节点就行了
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```



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
        // 首先要考虑头节点会不会变
        ListNode *dummy = new ListNode(-1, head);
        ListNode *fast = dummy, *slow = dummy;
        for (int i = 0; i < n; i++) {
            fast = fast->next;
        }
        while (fast != NULL && fast->next != NULL) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy->next;

    }
};
```



### [83. 删除排序链表中的重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/)

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *curr = head;
        while (curr != NULL) {
            while (curr->next != NULL && curr->val == curr->next->val) curr->next = curr->next->next;
            curr = curr->next;
        }
        return head;
    }
};
```





### [82. 删除排序链表中的重复元素 II](https://leetcode.cn/problems/remove-duplicates-from-sorted-list-ii/)

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *dummy = new ListNode(-1, head);
        ListNode *curr = dummy;
        while (curr) {
            if (curr->next != NULL && curr->next->next != NULL &&curr->next->val == curr->next->next->val) {
                int same = curr->next->val;
                while (curr->next != NULL && curr->next->val == same) {
                    curr->next = curr->next->next;
                }
            } 
            else {
                curr = curr->next;
            }
        }
        return dummy->next;
    }
};
```







## 二叉树 递归

栈这个数据结构就是最先进去的最后出来

### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

#### 递归做法

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
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

#### dfs做法


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
```



### [100. 相同的树](https://leetcode.cn/problems/same-tree/)

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == nullptr || q == nullptr) return p == q;
        return p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
        
    }
};
```



### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

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



### [110. 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)

#### 第一种：在递归地过程中维护树的平衡

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
    // 用-1来定义“不平衡”的树
    // 如果在某个点已经开始不平衡了，那么就要不断地往上返回-1
    int getHeight(TreeNode *root) {
        if (root == nullptr) return 0;
        int left = getHeight(root->left);
        if (left == -1) return -1;
        int right = getHeight(root->right);
        if (right == -1 || abs(left - right) > 1) return -1;
        return max(left, right) + 1;
    }
public:
    bool isBalanced(TreeNode* root) {
        return getHeight(root) != -1;
    }
};
```



#### 第二种：（一般的做法）每一次都去递归找出每个点的高度

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
    int height(TreeNode* root) {
        if (root == nullptr) return 0;
        return max(height(root->left), height(root->right)) + 1;
    }
public:
    bool isBalanced(TreeNode* root) {
        if (root == nullptr) return true;
        else {
            return abs(height(root->left) - height(root->right)) <= 1 && isBalanced(root->left) && isBalanced(root->right);
        }
    }
};
```



### [199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)

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
    vector<int>ans;
    void find(TreeNode* root, int d) {
        if (root == nullptr) return;
        if (d == ans.size()) ans.push_back(root->val);
        find(root->right, d + 1);
        find(root->left, d + 1);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        // 需要先递归右子树，然后再递归左子树
        // 写一个递归函数，如果这个节点的深度和答案的长度相等，那么需要将这个节点加入到答案中去
        find(root, 0);
        return ans;
    }
};
```

