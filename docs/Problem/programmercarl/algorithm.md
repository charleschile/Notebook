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





## 22. 二叉搜索树中的搜索（视频看过）

### [700. 二叉搜索树中的搜索](https://leetcode.cn/problems/search-in-a-binary-search-tree/)

使用递归的关键：递归是需要返回变量的

#### 递归法

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
    TreeNode* searchBST(TreeNode* root, int val) {
        if (root == NULL || root->val == val) return root;
        TreeNode* res;
        if (root->val < val) res = searchBST(root->right, val);
        if (root->val > val) res = searchBST(root->left, val);
        return res;
    }
};
```



#### 迭代法

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
    TreeNode* searchBST(TreeNode* root, int val) {
        if (root == NULL) return NULL;
        while (root) {
            if (root->val == val) return root;
            else if (root->val > val) root = root->left;
            else root = root->right;
        }
        return NULL;
    }
};
```



## 23.验证二叉搜索树（视频看过）



### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

#### 前序遍历(preorder traversal)

在每次递归的时候都是先访问根节点的值，确保根节点符合上面传过来的某种性质，然后再递归左子树和右子树



注意二叉搜索树中右边的所有的节点都需要大于根节点

比如5，4，6，null,null, 3, 7就是不合法的，因为3虽然比6小，但是需要比5大才行



所以我的思路是：（需要手动模拟！！！）

在向下的过程中，要维持住上方传递过来的最大值和最小值

在root向左走，max需要不断更新

在root向右走，min需要不断更新

![bst1](bst1.jpg)

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
        bool res = dfs(root, LONG_MIN, LONG_MAX);
        return res;
    }
    bool dfs(TreeNode* root, long min, long max) {
        if (root == NULL) return true;
        long x = root->val;
        return x > min && x < max && dfs(root->left, min, x) && dfs(root->right, x, max);
    }
};
```



#### 中序遍历(inorder traversal)

先遍历左子树，然后访问根节点，然后再遍历右子树

在整个遍历顺序中，根节点的访问总是在其左右子节点之后被访问，所以叫中序遍历 

在二叉搜索树中，如果在每个节点，都先遍历左子树，然后再遍历右子树，那么就能得到一个严格递增的数组



#### 中序遍历的第一种写法：维护一个数组

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
    vector<int> vec;
    bool isValidBST(TreeNode* root) {
        traseversal(root);
        for (int i = 0; i < vec.size() - 1; i++) {
            if (vec[i] >= vec[i + 1]) return false;
        }
        return true;
    }
    void traseversal(TreeNode* root) {
        if (root == NULL) return;
        traseversal(root->left);
        vec.push_back(root->val);
        traseversal(root->right);
    }
};
```



#### 中序遍历的第二种写法：维护上一个访问过的值

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
    long pre = LONG_MIN;
public:
    bool isValidBST(TreeNode* root) {
        if (root == NULL) return true;
        if (!isValidBST(root->left) || root->val <= pre) return false;
        pre = root->val;
        return isValidBST(root->right);
    }
};
```



#### 中序遍历的第三种写法：最直观的写法，并用双指针进行了优化，最推荐的写法！！！

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





#### 后序遍历

后序遍历就是先遍历左子树，然后遍历右子树，然后得出一个条件，最后访问根节点，看根节点是否符合这个得出的条件

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
    pair<long, long> dfs(TreeNode* root) {
        if (root == NULL) return {LONG_MAX, LONG_MIN};
        auto[l_min, l_max] = dfs(root->left);
        auto[r_min, r_max] = dfs(root->right);
        if (root->val <= l_max || root->val >= r_min) return {LONG_MIN, LONG_MAX};
        long x = root->val;
        return {min(x, l_min), max(x, r_max)};
    }
    bool isValidBST(TreeNode* root) {
        return dfs(root).second != LONG_MAX;
    }
};
```







## 24. 二叉搜索树的最小绝对差（视频看过）

### [530. 二叉搜索树的最小绝对差](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/)

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
    int difference = INT_MAX;
    TreeNode* pre = NULL;
public:
    int getMinimumDifference(TreeNode* root) {
        traseversal(root);
        return difference;
    }
    void traseversal(TreeNode* root) {
        if (root == NULL) return;
        traseversal(root->left);
        if (pre) {
            difference = min(difference, root->val - pre->val);
        } 
        pre = root;
        traseversal(root->right);
        
    }
};
```



## 25. 二叉搜索树中的众数

### [501. 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)

> 即使是在有重复数字的二叉搜索树中，中序遍历仍然是递增的数组！！！

mode是众数的意思

#### 中序遍历，只遍历一遍二叉搜索树，就求出众数的集合



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
    int count = 0;
    int maxCount = 0;
    vector<int> ans;
    void searchBST(TreeNode* root) {
        if (root == NULL) return;
        searchBST(root->left);

        if (pre == NULL) {
            count = 1;
        } else if (pre->val == root->val) {
            count++;
        } else {
            count = 1;
        }


        pre = root;

        
        if (count == maxCount) {
            ans.push_back(root->val);
        }

        if (count > maxCount) {
            maxCount = count;
            ans.clear();
            ans.push_back(root->val);
        }

        searchBST(root->right);
    }
    vector<int> findMode(TreeNode* root) {
        searchBST(root);
        return ans;
    }
};
```



#### 纯暴力，开哈希表记录（注意一下哈希表的语法），不推荐因为是算法题

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
    unordered_map<int, int> hash;
    int maxCount = 0;
    vector<int> ans;
public:
    vector<int> findMode(TreeNode* root) {
        dfs(root);
        for (unordered_map<int, int>::iterator it = hash.begin(); it != hash.end(); it++) {
            if (it->second == maxCount){
                ans.push_back(it->first);
            }
        }
        return ans;
    }
    void dfs(TreeNode* root) {
        if (root == NULL) return;
        maxCount = max(maxCount, ++hash[root->val]);
        dfs(root->left);
        dfs(root->right);
    }
};
```







## 26. 二叉树的最近公共祖先

### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

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





## 28. 二叉搜索树的最近公共祖先



### [235. 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)

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
        // 二叉搜索树的公共祖先相较于二叉树的公共祖先多了一个顺序
        // 可以直接提取p和q的value了

        // 只要p和q在root两边，那么最近公共祖先就必定是root
        if (p->val < root->val && q->val < root->val) return lowestCommonAncestor(root->left, p, q);
        if (p->val > root->val && q->val > root->val) return lowestCommonAncestor(root->right, p, q);
        return root;
    }
};
```





## 29. 二叉搜索树中的插入操作



### [701. 二叉搜索树中的插入操作](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)

注意写法的错误之处：

如果要插在temp->left那里，并且temp->left == NULL

千万不能:

```cpp
temp = temp->left;
temp = new TreeNode(val);
```

这样的话temp->left并没有指向新的节点

而必须要：

```cpp
temp->left = new TreeNode(val);
```



#### 需要掌握的递归写法

而需要一个函数就搞定递归的话，就需要在需要插入的地方返回新建的TreeNode，而在不需要插入的时候返回原来的根节点

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
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root == NULL) return new TreeNode(val);
        if (root->val < val) root->right = insertIntoBST(root->right, val);
        if (root->val > val) root->left = insertIntoBST(root->left, val);
        return root;
    }
};
```





#### 最直白的迭代写法，不推荐

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
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root == NULL) return new TreeNode(val);
        TreeNode* temp = root;
        TreeNode* parent = root; // 这个很重要，需要记录上一个节点，否则无法赋值新节点
        while (temp) {
            parent = temp;
            if (val > temp->val) temp = temp->right;
            else temp = temp->left;
        }
        if (val > parent->val) parent->right = new TreeNode(val); // 此时是用parent节点的进行赋值
        else parent->left = new TreeNode(val);
        return root;
    }
};
```





## 30. 删除二叉搜索树中的节点



### [450. 删除二叉搜索树中的节点](https://leetcode.cn/problems/delete-node-in-a-bst/)

>  对于二叉树中各种操作，返回`TreeNode*`的理解是返回的是下面已经处理好的节点
>
> 返回的节点相当于在告诉上面一层：“从我下面开始的东西都已经处理好了！”

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
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (root == NULL) return NULL;
        if (root->val == key) {
            if (root->left == NULL && root->right == NULL) {
                delete root;
                // 相当于删除了节点，那么这个地方会变成null
                return NULL;
            } 
            else if (root->left == NULL) {
                TreeNode* returnNode = root->right;
                delete root;
                return returnNode;
            }
            else if (root->right == NULL) {
                TreeNode* returnNode = root->left;
                delete root;
                return returnNode;
            }
            else {
                // 如果我们要删除一个左右都有儿子的节点（包括根节点）
                // 我们的策略是返回root->right
                // 而root->left应该比root->left里面的最小值还要小
                TreeNode* returnNode = root->right;
                TreeNode* curr = root->right;
                while (curr->left != NULL) {
                    curr = curr->left;
                }
                curr->left = root->left;
                delete root;
                return returnNode;
            }
        }
        // 如果root并不等于key，那么肯定不能直接返回root
        // 而是要对root的left和right进行处理一下，处理好了之后才能返回root给上面一层
        if (root->val > key) root->left = deleteNode(root->left, key);
        if (root->val < key) root->right = deleteNode(root->right, key);

        return root;

    }
};
```











## 31. 修剪二叉搜索树

### [669. 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree/)

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
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        // 假设一个root小于low，那么他的左儿子可以放弃，而右儿子需要被继承
        // 假设一个root大于high，那么他的右儿子可以放弃，只剩下左儿子
        // 对于修剪二叉树来说，只要略过那些不需要的子树就行了，并没有对各个节点做什么操作，最后返回的也是根节点的值
        if (root == NULL) return NULL;
        if (root->val < low) return trimBST(root->right, low, high);
        if (root->val > high) return trimBST(root->left, low, high);
        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        return root;
    }
};
```









## 灵茶山艾府课程













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


template <typename T>
class SinglyLinkedList {
private:
    class Node {
    public:
        T data;
        Node* next;
    };

    Node* head;
    size_t size;

public:
    // Constructors
    SinglyLinkedList();
    SinglyLinkedList(const T& initialData);

    // Other methods
    void pushFront(const T& value);
    void popFront();
    bool isEmpty() const;
    size_t getSize() const;
    // Add more methods as needed
};

template <typename T>
class SinglyLinkedList {
private:
    class Node {
    public:
        T data;
        Node* next;
        Node(const T& value) : data(value), next(nullptr) {}
    };

    Node* head;
    size_t size;

public:
    // Constructors
    SinglyLinkedList() : head(nullptr), size(0) {}

    SinglyLinkedList(const T& initialValue) : head(nullptr), size(0) {
        pushFront(initialValue);
    }

    // Destructor
    ~SinglyLinkedList() {
        while (head) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Public methods
    void pushFront(const T& value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
        size++;
    }

    void popFront() {
        if (head) {
            Node* temp = head;
            head = head->next;
            delete temp;
            size--;
        }
    }

    void append(const T& value) {
        Node* newNode = new Node(value);
        if (!head) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next) {
                current = current->next;
            }
            current->next = newNode;
        }
        size++;
    }

    // Other methods like insert, remove, search, size, print, etc.
    // ...

    // Getter for size
    size_t getSize() const {
        return size;
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







## 验证二叉搜索树

### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

#### 前序遍历

在整个遍历的过程中，先访问节点的值（判断是否符合上面传下来的要求）再递归左右子树的做法叫做前序遍历

最便捷写法

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
    bool isValidBST(TreeNode* root, long left = LONG_MIN, long right = LONG_MAX) {
        if (root == nullptr) return true;
        long x= root->val;
        return left < x && x < right && isValidBST(root->left, left, x) && isValidBST(root->right, x, right);
    }
};
```



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
    // 这个函数维持的是每个节点需要大于的值（left）和需要小于的值（right）
    bool dfs(TreeNode* root, long left, long right) {
        if (!root) return true;
        if (root->val <= left || root->val >= right) return false;
        // 因为root的左儿子需要小于root的值，所以更新right
        return dfs(root->left, left, root->val) && dfs(root->right, root->val, right);
    }
public:
    bool isValidBST(TreeNode* root) {
        return dfs(root, LONG_MIN, LONG_MAX);
    }
};
```



#### 前序遍历第三种写法

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
    vector<int> dfs(TreeNode* root) {
        vector<int> res = {1, root->val, root->val};
        if (root->left) {
            vector<int> t = dfs(root->left);
            if (root->val <= t[2] || t[0] == 0) res[0] = 0;
            res[1] = min(t[1], res[1]);
            res[2] = max(t[2], res[2]);
        }
        if (root->right) {
            vector<int> t = dfs(root->right);
            if (root->val >= t[1] || t[0] == 0) res[0] = 0;
            res[1] = min(t[1], res[1]);
            res[2] = max(t[2], res[2]);
        }
        return res;
    }
public:
    bool isValidBST(TreeNode* root) {
        if (!root) return false;
        return dfs(root)[0];
    }
};
```



#### 中序遍历

如果在每个节点，都先遍历左子树，然后再遍历右子树，那么就能得到一个严格递增的数组

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
    long pre = LONG_MIN;
public:
    // 中序遍历
    // 由于这里的代码时先执行!isValidBST这一步的，所以这里是先沿着左子树一路向下，然后再是右子树
    // 所以遍历到的值有单调递增的性质
    // 而全局变量pre维护的就是一路上的最大值，而所有被遍历到的节点，无论是左子树还是右子树都需要比遍历到时的最大值pre大就行了
    bool isValidBST(TreeNode* root) {
        if (root == nullptr) {
            return true;
        }
        if (!isValidBST(root->left) || root->val <= pre) return false;
        pre = root->val;
        return isValidBST(root->right);
    }
};
```



#### 后续遍历

在后序遍历中，递归调用发生在处理当前节点之前





注意结构化绑定本身是与auto关联紧密的语法特性，如果不使用auto，就不要使用结构化绑定

结构化绑定的用法：`auto[l_min, l_max] = dfs(node->left);`

如果不使用auto和结构化绑定的话，就要使用：

````cpp
pair<long, long> left_result = dfs(node->left);
        long l_min = left_result.first;
        long l_max = left_result.second;
````



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
    pair<long, long> dfs(TreeNode* root) {
        // 注意：碰到空节点返回的是{LONG_MAX, LONG_MIN}
        if (root == nullptr) return {LONG_MAX, LONG_MIN};
        auto[l_min, l_max] = dfs(root->left);
        auto[r_min, r_max] = dfs(root->right);
        long x = root->val;
        // 而碰到错误的返回就是{LONG_MIN, LONG_MAX}，这样只要有错，上面的节点就都是错误的
        if (x <= l_max || x >= r_min) return {LONG_MIN, LONG_MAX};
        return {min(l_min, x), max(r_max, x)};

    }
public:
    bool isValidBST(TreeNode* root) {
        return dfs(root).second != LONG_MAX;
    }
};mo
```



前序遍历（Preorder Traversal），中序遍历（Inorder Traversal）和后序遍历（Postorder Traversal）都是二叉树的不同遍历方式，它们的区别在于节点的访问顺序。

1. **前序遍历**：

   - 访问当前节点。
   - 递归遍历左子树。
   - 递归遍历右子树。

   用例子来说明，考虑以下二叉树：

   ```
       1
      / \
     2   3
    / \
   4   5
   ```

   前序遍历结果：1 -> 2 -> 4 -> 5 -> 3

2. **中序遍历**：

   - 递归遍历左子树。
   - 访问当前节点。
   - 递归遍历右子树。

   用例子来说明，同样的二叉树：

   中序遍历结果：4 -> 2 -> 5 -> 1 -> 3

3. **后序遍历**：

   - 递归遍历左子树。
   - 递归遍历右子树。
   - 访问当前节点。

   再次以相同的二叉树为例：

   后序遍历结果：4 -> 5 -> 2 -> 3 -> 1

这三种遍历方式分别描述了在遍历二叉树时访问节点的不同顺序。前序遍历从根节点开始，然后依次遍历左子树和右子树。中序遍历首先遍历左子树，然后访问当前节点，最后遍历右子树。后序遍历首先遍历左子树，然后遍历右子树，最后访问当前节点。





### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

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
        if (root == nullptr || root == p || root == q) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left == nullptr) return right;
        if (right == nullptr) return left; 
        // 两边都有的情况只能有一种：那就是他们的最近公共祖先
        return root;
    }
};
```



### [235. 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)

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
        // 因为是二叉搜索树，那么没有两个节点会相同的值，并且具有单调性
        int x = root->val;
        if (p->val < x && q->val < x) return lowestCommonAncestor(root->left, p, q);
        if (p->val > x && q->val > x) return lowestCommonAncestor(root->right, p, q);
        // 如果p和q一个比root大，一个比root小，那么root必定是他们的最近公共祖先，没有例外！
        return root;
    }
};
```



## 二叉树的层序遍历

### [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

#### 使用普通的vector

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
        vector<TreeNode*> curr = {root};
        while (curr.size()) {
            vector<TreeNode*> nxt;
            vector<int> vals;
            for (TreeNode* node : curr) {
                vals.push_back(node->val);
                if (node->left) nxt.push_back(node->left);
                if (node->right) nxt.push_back(node->right);
            }
            curr = move(nxt);
            ans.emplace_back(vals);
        }
        return ans;

    }
};
```



#### 使用队列

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
        if (root == nullptr) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> curr;
        curr.push(root);
        while (!curr.empty()) {
            vector<int> vals;
            for (int n = curr.size(); n > 0; n--) {
                auto node = curr.front();
                curr.pop();
                vals.push_back(node->val);
                if (node->left) curr.push(node->left);
                if (node->right) curr.push(node->right);  
            }
            ans.emplace_back(vals);
        }
        return ans;
    }
    
};
```







### [103. 二叉树的锯齿形层序遍历](https://leetcode.cn/problems/binary-tree-zigzag-level-order-traversal/)

### 使用vector

注意使用emplace_back()，效率会比push_back()高很多

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (root == nullptr) return {};
        vector<vector<int>> ans;
        vector<TreeNode*> curr = {root};
        for (bool even = false; !curr.empty(); even = !even) {
            vector<TreeNode*> next;
            vector<int> vals;
            for (TreeNode* node : curr) {
                vals.push_back(node->val);
                if (node->left) next.push_back(node->left);
                if (node->right) next.push_back(node->right);
            }
            curr = move(next);
            if (even) reverse(vals.begin(), vals.end());
            ans.emplace_back(vals);
        }
        return ans;
    }
};
```



#### 使用队列

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (root == nullptr) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> curr;
        curr.push(root);
        for (bool even = false; !curr.empty(); even = !even) {
            vector<int> vals;
            for (int i = curr.size(); i > 0; i--) {
                TreeNode* node = curr.front();
                curr.pop();
                vals.push_back(node->val);
                if (node->left) curr.push(node->left);
                if (node->right) curr.push(node->right);
            }
            if (even) reverse(vals.begin(), vals.end());
            ans.emplace_back(vals);
        }
        return ans;
    }
};
```



### [513. 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)

#### 从左到右遍历，然后最后一层的第一个就是

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
    int findBottomLeftValue(TreeNode* root) {
        int ans;
        queue<TreeNode*> curr;
        curr.push(root);
        while (!curr.empty()) {
            ans = curr.front()->val;
            for (int i = curr.size(); i > 0; i--) {
                TreeNode* node = curr.front();
                curr.pop();
                if (node->left) curr.push(node->left);
                if (node->right) curr.push(node->right);
            }
        }
        return ans;
    }
};
```



#### 从右往左遍历

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
    int findBottomLeftValue(TreeNode* root) {
        int ans;
        queue<TreeNode*> curr;
        curr.push(root);
        while (!curr.empty()) {
            ans = curr.front()->val;
            for (int i = curr.size(); i > 0; i--) {
                TreeNode* node = curr.front();
                curr.pop();
                if (node->left) curr.push(node->left);
                if (node->right) curr.push(node->right);
            }
        }
        return ans;
    }
};
```





## 回溯算法套路1：子集型回归

原问题：构造一个长度为n的字符串

过程：枚举一个字母

子问题：构造一个长度为n-1的字符串



当子问题和原问题是相似的，这种从原问题到子问题的过程适合用递归解决

回溯有一个增量构造答案的过程，这个过程通常用递归实现

只要将边界条件和非边界条件逻辑写对，就能保证写的算法是对的



回溯问题的做法：

用一个path数组记录路径上的字母

回溯三问：

1. 当前操作，枚举path[i]要填入的字母
2. 子问题？构造字符串>= i的部分
3. 下一个子问题？构造字符串>= i + 1的部分

dfs(i) -> dfs(i + 1)，这里的i的意思是考虑到了>= i 的部分



### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

#### acwing写法

```cpp
class Solution {
public:
    vector<string> ans;
    vector<string> map = {
        "", "", "abc", "def",
        "ghi", "jkl", "mno",
        "pqrs", "tuv", "wxyz"
    };
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return ans;
        dfs(digits, 0, "");
        return ans;
    }
    void dfs(string& digits, int n, string path) {
        if (n == digits.size()) {
            ans.push_back(path);
        }
        else {
            for (char c : map[digits[n] - '0']) {
                dfs(digits, n + 1, path + c);
            }
        }
    }
};
```



#### 灵茶山艾府写法

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

























### [78. 子集](https://leetcode.cn/problems/subsets/)



#### 将function写在外面，比较麻烦，不推荐

```cpp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> ans;
    vector<vector<int>> subsets(vector<int>& nums) {
        int k = nums.size();
        dfs(0, k,nums);
        return ans;
    }
    void dfs(int n, int k, vector<int>& nums) {
        if (n == k) {
            ans.push_back(path);
        }
        else {
            dfs(n + 1, k, nums);
            path.push_back(nums[n]);
            dfs(n + 1, k, nums);
            path.pop_back();
        }
    }
};
```



#### lambda函数，写在里面，推荐

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> path;
        vector<vector<int>> ans;
        int u = nums.size();
        function<void(int)> dfs = [&] (int i) {
            if (i == u) {
                ans.push_back(path);
                return;
            }
            else {
                dfs(i + 1);
                path.push_back(nums[i]);
                dfs(i + 1);
                path.pop_back();
            }
        };
        dfs(0);
        return ans;
    }
};
```



#### 枚举递归

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> path;
        vector<vector<int>> ans;
        int u = nums.size();
        function<void(int)> dfs = [&] (int i) {
            ans.push_back(path);
            if (i == u) {
                return;
            }
            for (int j = i; j < u; j ++) {
                path.push_back(nums[j]);
                dfs(j + 1);
                path.pop_back();
            }
            
        };
        dfs(0);
        return ans;
    }
};
```



## 组合型回溯 剪枝

### [77. 组合](https://leetcode.cn/problems/combinations/)

### 灵茶山艾府做法+剪枝

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> ans;
        vector<int> path;
        function<void(int)> dfs = [&] (int i) {
            int d = k - path.size(); // d是还需要多少个
            if (d == 0) {
                ans.emplace_back(path);
                return;
            }
            for (int j = i; j >= d; j--) {
                path.push_back(j);
                dfs(j - 1);
                path.pop_back();
            }
        };
        dfs(n);
        return ans;
    }
};
```





#### dfs过程中枚举下一个数选哪个

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> ans;
        vector<int> path;
        function<void(int, int)> dfs = [&] (int start, int curr) {
            if (curr == k) {
                ans.emplace_back(path);
                return;
            }
            for (int i = start; i <= n; i++) {
                path.push_back(i);
                dfs(i + 1, curr + 1);
                path.pop_back();
            }
        };
        dfs(1, 0);
        return ans;
    }
};
```





#### 选或者不选的做法



```cpp
class Solution {
public:
void dfs(int u, int curr) {

}
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> ans;
        vector<int> path;
        function<void(int, int)> dfs = [&] (int u, int curr) {
            if (curr == k) {
                ans.emplace_back(path);
                return;
            }
            if (u <= n) dfs(u + 1, curr);
            path.push_back(u);
            if (u <= n) dfs(u + 1, curr + 1);
            path.pop_back();
        };
        dfs(1, 0);
        return ans;
    }
};
```



### [216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)

#### 枚举下个数选哪个

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> ans;
        vector<int> path;
        function<void(int, int)> dfs = [&] (int i, int t) {
            int d = k - path.size();
            if (t < 0 || t > (i + i - d + 1) * d / 2) return;
            if (d == 0) {
                ans.emplace_back(path);
                return;
            }
            for (int j = i; j >= d; --j) {
                path.push_back(j);
                dfs(j - 1, t - j);
                path.pop_back();
            }
            
        };
        dfs(9, n);
        return ans;
    }
};
```







#### 选或不选的做法



```cpp
class Solution {
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> ans;
        vector<int> path;
        function<void(int, int)> dfs = [&] (int t, int u) {
            int d = k - path.size();
            if (d == 0 && t == 0) {
                ans.emplace_back(path);
                return;
            }
            // 需要剪枝
            // 如果target小于0了直接返回
            // 如果接下来的连续最大的和都达不到target的话，也直接返回
            if (t < 0 || t > (u + u - d + 1) * d / 2) return;
            // 使用选择与否来做
            // 剪枝：如果剩下的个数不足也直接return
            // 不选择现在这个数
            // 因为剩下的每个数都选择的话，u现在的最小值是d + 1，所以这里的条件是u>d
            if (u > d) dfs(t, u - 1);
            // 选择现在这个数
            // 而剩下的每个数都选择的话，并且选择现在这个数，那么u最小是d
            // 如果d>u的话，回漏掉一种情况
            if (u >= d) {
                path.push_back(u);
                t -= u;
                dfs(t, u - 1);
                t += u;
                path.pop_back();
            }
        };
        dfs(n, 9);
        return ans;
    }
};
```





### [22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)

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



### [301. 删除无效的括号](https://leetcode.cn/problems/remove-invalid-parentheses/)

合法括号序列需要满足的条件：

1. 左右括号数量相同
2. 括号序列任意一个前缀中左括号数量>=右括号数量



l表示当前左括号数量比右括号数量多多少个

r表示当前要删掉多少个右括号

循环结束时，l表示要删掉的左括号的数量，r表示要删掉的额右括号的数量

#### acwing写法

```cpp
class Solution {
public:
    vector<string> ans;
    vector<string> removeInvalidParentheses(string s) {
        int l = 0, r = 0;
        for (auto x : s) {
            if (x == '(') l++;
            else if (x == ')') {
                if (l == 0) r++;
                else l--;
            }
        }
        dfs(s, 0, "", 0, l, r);
        return ans;
    }
    void dfs(string& s, int u, string path, int cnt, int l, int r) {
        if (u == s.size()) {
            if (!cnt) ans.push_back(path);
            return;
        }
        if (s[u] != '(' && s[u] != ')') dfs(s, u + 1, path + s[u], cnt, l, r);
        else if (s[u] == '(') {
            int k = u;
            while (k < s.size() && s[k] == '(') k++;
            l -= k -u;
            // for-loop里是枚举k-u+1种可能，从k-u个字符全删，到k-u个字符全留。人为规定这种顺序，目的在于剪枝。
            // 每次dfs()完后，不论有没有有效path，都会回溯到上层dfs()，可理解为恢复现场。
            for (int i = k - u; i >= 0; i--) {
                if (l >= 0) dfs(s, k, path, cnt, l, r);
                path += '(';
                cnt++, l++;
            }
        } else if (s[u] == ')') {
            int k = u;
            while (k < s.size() && s[k] == ')') k++;
            r -= k - u;
            for (int i = k - u; i >= 0; i--) {
                if (cnt >= 0 && r >= 0) dfs(s, k, path, cnt, l, r);
                path += ')';
                cnt--, r++;
            }
        }
    }
};
```



#### 力扣网友写法（抄的，还没自己实践）

```cpp
class Solution {
public:
    unordered_set<string> unique;
    vector<string> removeInvalidParentheses(string s) {
        vector<string> ans;
        int l = 0; // 左括号需要删除的数量；
        int r = 0; // 右括号需要删除的数量；
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') l++; // 遇到左括号计数；如果有匹配的右括号，可以抵消；
            // 抵消不了的都是我们需要删除的左括号
            else if (s[i] == ')') {
                // 左括号为0；此时遇到右括号一定是匹配不了的，需要删除的
                if (l == 0) r++;
                
                // 匹配掉一个左括号，相当于出栈
                else l--;
            }
            
        }
        string t = "";
        dfs(s, t, 0, l, r, 0, 0);
        for (auto s : unique) {
            ans.emplace_back(s);
        }
        return ans;
    }
    void dfs(string& s, string& t, int i, int l, int r, int lcnt, int rcnt) {
        if (i == s.size()) {
            // 递归终点； 用set去重
            if (l == 0 && r == 0) unique.insert(t);
            return;
        }
        // 跳过左右括号，但剩下需要删除的括号不能小于0
        if (s[i] == '(' && l > 0) {
            dfs(s, t, i + 1, l - 1, r, lcnt, rcnt);
        }
        if (s[i] == ')' && r > 0) {
            dfs(s, t, i + 1, l, r - 1, lcnt, rcnt);
        }
         // 保留当前字符；可能是括号，也可能是字母
        t.push_back(s[i]);
        if (s[i] != '(' && s[i] != ')') {
            // 如果是字母，不用处理
            dfs(s, t, i + 1, l, r, lcnt, rcnt);
        } else if (s[i] == '(') {
            // 如果是左括号，我们更新左括号的数量
            dfs(s, t, i + 1, l, r, lcnt + 1, rcnt);
        } else if (s[i] == ')' && rcnt < lcnt) {
            // 这一步实际上是把右括号多余的分支剪除； 只有 rcnt < lcnt 我们才有必要继续递归
            // 避免出现 `)(` 这样的情况
            dfs(s, t, i + 1, l, r, lcnt, rcnt + 1);
        }
        // 恢复现场
        t.pop_back();
    }
};
```



 



