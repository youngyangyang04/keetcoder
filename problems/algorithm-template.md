# Algorithm Templates

## Algorithm Templates

### Binary Search

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0;
        int right = n; // Define target in the left-closed, right-open interval [left, right)  
        while (left < right) { // When left == right, [left, right) is invalid
            int middle = left + ((right - left) >> 1);
            if (nums[middle] > target) {
                right = middle; // Target is in the left interval, since it is a left-closed, right-open interval, nums[middle] is not the target, so right = middle, continue searching in [left, middle)
            } else if (nums[middle] < target) {
                left = middle + 1; // Target is in the right interval, in [middle+1, right)
            } else { // nums[middle] == target
                return middle; // Target found in the array, return the index
            }
        }
        return right;
    }
};
```

### KMP

```cpp
void kmp(int* next, const string& s){
    next[0] = -1;
    int j = -1;
    for(int i = 1; i < s.size(); i++){
        while (j >= 0 && s[i] != s[j + 1]) {
            j = next[j];
        }
        if (s[i] == s[j + 1]) {
            j++;
        }
        next[i] = j;
    }
}
```

### Binary Tree

Definition of a binary tree:

```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
```

#### Depth-First Search (Recursive)

Preorder traversal (Root-Left-Right)
```cpp
void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    vec.push_back(cur->val);    // Process node
    traversal(cur->left, vec);  // Left
    traversal(cur->right, vec); // Right
}
```
Inorder traversal (Left-Root-Right)
```cpp
void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    traversal(cur->left, vec);  // Left
    vec.push_back(cur->val);    // Process node
    traversal(cur->right, vec); // Right
}
```
Postorder traversal (Left-Right-Root)
```cpp
void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    traversal(cur->left, vec);  // Left
    traversal(cur->right, vec); // Right
    vec.push_back(cur->val);    // Process node
}
```

#### Depth-First Search (Iterative)

Related solution: [0102.Binary Tree Level Order Traversal](https://keetcoder.com/problems/0102.binary-tree-level-order-traversal.html)

Preorder traversal (Root-Left-Right)
```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> st;
    if (root != NULL) st.push(root);
    while (!st.empty()) {
        TreeNode* node = st.top();
        if (node != NULL) {
            st.pop();
            if (node->right) st.push(node->right);  // Right
            if (node->left) st.push(node->left);    // Left
            st.push(node);                          // Root
            st.push(NULL);                          
        } else {
            st.pop();
            node = st.top();
            st.pop();
            result.push_back(node->val);            // Process node
        }
    }
    return result;
}
```

Inorder traversal (Left-Root-Right)
```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result; // Store inorder elements
    stack<TreeNode*> st;
    if (root != NULL) st.push(root);
    while (!st.empty()) {
        TreeNode* node = st.top();
        if (node != NULL) {
            st.pop(); 
            if (node->right) st.push(node->right);  // Right
            st.push(node);                          // Root
            st.push(NULL); 
            if (node->left) st.push(node->left);    // Left
        } else {
            st.pop(); 
            node = st.top(); 
            st.pop();
            result.push_back(node->val);            // Process node
        }
    }
    return result;
}
```

Postorder traversal (Left-Right-Root)
```cpp
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> st;
    if (root != NULL) st.push(root);
    while (!st.empty()) {
        TreeNode* node = st.top();
        if (node != NULL) {
            st.pop();
            st.push(node);                          // Root
            st.push(NULL);
            if (node->right) st.push(node->right);  // Right
            if (node->left) st.push(node->left);    // Left

        } else {
            st.pop();
            node = st.top();
            st.pop();
            result.push_back(node->val);            // Process node
        }
    }
    return result;
}
```
#### Breadth-First Search (Queue)

Related solution: [0102.Binary Tree Level Order Traversal](https://keetcoder.com/problems/0102.binary-tree-level-order-traversal.html)

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    queue<TreeNode*> que;
    if (root != NULL) que.push(root);
    vector<vector<int>> result;
    while (!que.empty()) {
        int size = que.size();
        vector<int> vec;
        for (int i = 0; i < size; i++) { // Use fixed size, not que.size()
            TreeNode* node = que.front();
            que.pop();
            vec.push_back(node->val);   // Process node
            if (node->left) que.push(node->left);
            if (node->right) que.push(node->right);
        }
        result.push_back(vec);
    }
    return result;
}
```

Problems solvable directly with the above method:

* [0102.Binary Tree Level Order Traversal](https://keetcoder.com/problems/0102.binary-tree-level-order-traversal.html)
* [0199.Binary Tree Right Side View](https://github.com/youngyangyang04/leetcode/blob/master/problems/0199.二叉树的右视图.md)
* [0637.Average of Levels in Binary Tree](https://github.com/youngyangyang04/leetcode/blob/master/problems/0637.二叉树的层平均值.md) 
* [0104.Maximum Depth of Binary Tree (Iterative Method)](https://keetcoder.com/problems/0104.maximum-depth-of-binary-tree.html)
* [0111.Minimum Depth of Binary Tree (Iterative Method)](https://keetcoder.com/problems/0111.minimum-depth-of-binary-tree.html)
* [0222.Count Complete Tree Nodes (Iterative Method)](https://keetcoder.com/problems/0222.count-complete-tree-nodes.html)

#### Binary Tree Depth

```cpp
int getDepth(TreeNode* node) {
    if (node == NULL) return 0;
    return 1 + max(getDepth(node->left), getDepth(node->right));
}
```

#### Binary Tree Node Count

```cpp
int countNodes(TreeNode* root) {
    if (root == NULL) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```

### Backtracking Algorithm 
```cpp
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

### Union-Find 

```cpp
    int n = 1005; // Define according to the problem statement 
    int father[1005];

    // Union-Find initialization
    void init() {
        for (int i = 0; i < n; ++i) {
            father[i] = i;
        }
    }
    // Find the root in the Union-Find structure
    int find(int u) {
        return u == father[u] ? u : father[u] = find(father[u]);
    }
    // Add the edge v->u to the Union-Find
    void join(int u, int v) {
        u = find(u);
        v = find(v);
        if (u == v) return ;
        father[v] = u;
    }
    // Check if u and v share the same root
    bool same(int u, int v) {
        u = find(u);
        v = find(v);
        return u == v;
    }
```

(Continuously updating)
## Other Language Versions

### JavaScript:

#### Binary Search

Using left-closed, right-closed interval

```javascript
var search = function (nums, target) {
    let left = 0, right = nums.length - 1;
    // Use left-closed, right-closed interval
    while (left <= right) {
        let mid = left + Math.floor((right - left)/2);
        if (nums[mid] > target) {
            right = mid - 1;  // Look in the left closed interval
        } else if (nums[mid] < target) {
            left = mid + 1;   // Look in the right closed interval
        } else {
            return mid;
        }
    }
    return -1;
};
```

Using left-closed, right-open interval

```javascript
var search = function (nums, target) {
    let left = 0, right = nums.length;
    // Use left-closed, right-open interval [left, right)
    while (left < right) {
        let mid = left + Math.floor((right - left)/2);
        if (nums[mid] > target) {
            right = mid;  // Look in the left closed interval
        } else if (nums[mid] < target) {
            left = mid + 1;   // Look in the right closed interval
        } else {
            return mid;
        }
    }
    return -1;
};
```

#### KMP

```javascript
var kmp = function (next, s) {
    next[0] = -1;
    let j = -1;
    for(let i = 1; i < s.length; i++){
        while (j >= 0 && s[i] !== s[j + 1]) {
            j = next[j];
        }
        if (s[i] === s[j + 1]) {
            j++;
        }
        next[i] = j;
    }
}
```

#### Binary Tree

##### Depth-First Search (Recursive)

Binary tree node definition:

```javascript
function TreeNode (val, left, right) {
    this.val = (val === undefined ? 0 : val);
    this.left = (left === undefined ? null : left);
    this.right = (right === undefined ? null : right);
}
```

Preorder traversal (Root-Left-Right):

```javascript
var preorder = function (root, list) {
    if (root === null) return;
    list.push(root.val);        // Root
    preorder(root.left, list);  // Left
    preorder(root.right, list); // Right
}
```

Inorder traversal (Left-Root-Right):

```javascript
var inorder = function (root, list) {
    if (root === null) return;
    inorder(root.left, list);  // Left
    list.push(root.val);        // Root
    inorder(root.right, list); // Right
}
```

Postorder traversal (Left-Right-Root):

```javascript
var postorder = function (root, list) {
    if (root === null) return;
    postorder(root.left, list);  // Left
    postorder(root.right, list); // Right
    list.push(root.val);        // Root
}
```

##### Depth-First Search (Iterative)

Preorder traversal (Root-Left-Right):

```javascript
var preorderTraversal = function (root) {
    let res = [];
    if (root === null) return res;
    let stack = [root],
        cur = null;
    while (stack.length) {
        cur = stack.pop();
        res.push(cur.val);
        cur.right && stack.push(cur.right);
        cur.left && stack.push(cur.left);
    }
    return res;
};
```

Inorder traversal (Left-Root-Right):

```javascript
var inorderTraversal = function (root) {
    let res = [];
    if (root === null) return res;
    let stack = [];
    let cur = root;
    while (stack.length !== 0 || cur !== null) {
        if (cur !== null) {
            stack.push(cur);
            cur = cur.left;
        } else {
            cur = stack.pop();
            res.push(cur.val);
            cur = cur.right;
        }
    }
    return res;
};
```

Postorder traversal (Left-Right-Root):

```javascript
var postorderTraversal = function (root) {
    let res = [];
    if (root === null) return res;
    let stack = [root];
    let cur = null;
    while (stack.length) {
        cur = stack.pop();
        res.push(cur.val);
        cur.left && stack.push(cur.left);
        cur.right && stack.push(cur.right);
    }
    return res.reverse()
};
```

##### Breadth-First Search (Queue)

```javascript
var levelOrder = function (root) {
    let res = [];
    if (root === null) return res;
    let queue = [root];
    while (queue.length) {
        let n = queue.length;
        let temp = [];
        for (let i = 0; i < n; i++) {
            let node = queue.shift();
            temp.push(node.val);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        res.push(temp);
    }
    return res;
};
```

##### Binary Tree Depth

```javascript
var getDepth = function (node) {
    if (node === null) return 0;
    return 1 + Math.max(getDepth(node.left), getDepth(node.right));
}
```

##### Binary Tree Node Count

```javascript
var countNodes = function (root) {
    if (root === null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

#### Backtracking Algorithm 

```javascript
function backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

#### Union-Find 

```javascript
    let n = 1005; // Define according to the problem statement 
    let father = new Array(n).fill(0);

    // Union-Find initialization
    function init () {
        for (int i = 0; i < n; ++i) {
            father[i] = i;
        }
    }
    // Find the root in the Union-Find structure
    function find (u) {
        return u === father[u] ? u : father[u] = find(father[u]);
    }
    // Add the edge v->u to the Union-Find
    function join(u, v) {
        u = find(u);
        v = find(v);
        if (u === v) return ;
        father[v] = u;
    }
    // Check if u and v share the same root
    function same(u, v) {
        u = find(u);
        v = find(v);
        return u === v;
    }
```

### TypeScript:

#### Binary Search

Using left-closed, right-closed interval

```typescript
var search = function (nums: number[], target: number): number {
    let left: number = 0, right: number = nums.length - 1;
    // Use left-closed, right-closed interval
    while (left <= right) {
        let mid: number = left + Math.floor((right - left)/2);
        if (nums[mid] > target) {
            right = mid - 1;  // Look in the left closed interval
        } else if (nums[mid] < target) {
            left = mid + 1;   // Look in the right closed interval
        } else {
            return mid;
        }
    }
    return -1;
};
```

Using left-closed, right-open interval

```typescript
var search = function (nums: number[], target: number): number {
    let left: number = 0, right: number = nums.length;
    // Use left-closed, right-open interval [left, right)
    while (left < right) {
        let mid: number = left + Math.floor((right - left)/2);
        if (nums[mid] > target) {
            right = mid;  // Look in the left closed interval
        } else if (nums[mid] < target) {
            left = mid + 1;   // Look in the right closed interval
        } else {
            return mid;
        }
    }
    return -1;
};
```

#### KMP

```typescript
var kmp = function (next: number[], s: number): void {
    next[0] = -1;
    let j: number = -1;
    for(let i: number = 1; i < s.length; i++){
        while (j >= 0 && s[i] !== s[j + 1]) {
            j = next[j];
        }
        if (s[i] === s[j + 1]) {
            j++;
        }
        next[i] = j;
    }
}
```

#### Binary Tree

##### Depth-First Search (Recursive)

Binary tree node definition:

```typescript
class TreeNode {
    val: number
    left: TreeNode | null
    right: TreeNode | null
    constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
        this.val = (val===undefined ? 0 : val)
        this.left = (left===undefined ? null : left)
        this.right = (right===undefined ? null : right)
    }
}
```

Preorder traversal (Root-Left-Right):

```typescript
var preorder = function (root: TreeNode | null, list: number[]): void {
    if (root === null) return;
    list.push(root.val);        // Root
    preorder(root.left, list);  // Left
    preorder(root.right, list); // Right
}
```

Inorder traversal (Left-Root-Right):

```typescript
var inorder = function (root: TreeNode | null, list: number[]): void {
    if (root === null) return;
    inorder(root.left, list);  // Left
    list.push(root.val);        // Root
    inorder(root.right, list); // Right
}
```

Postorder traversal (Left-Right-Root):

```typescript
var postorder = function (root: TreeNode | null, list: number[]): void {
    if (root === null) return;
    postorder(root.left, list);  // Left
    postorder(root.right, list); // Right
    list.push(root.val);        // Root
}
```

##### Depth-First Search (Iterative)

Preorder traversal (Root-Left-Right):

```typescript
var preorderTraversal = function (root: TreeNode | null): number[] {
    let res: number[] = [];
    if (root === null) return res;
    let stack: TreeNode[] = [root],
        cur: TreeNode | null = null;
    while (stack.length) {
        cur = stack.pop();
        res.push(cur.val);
        cur.right && stack.push(cur.right);
        cur.left && stack.push(cur.left);
    }
    return res;
};
```

Inorder traversal (Left-Root-Right):

```typescript
var inorderTraversal = function (root: TreeNode | null): number[] {
    let res: number[] = [];
    if (root === null) return res;
    let stack: TreeNode[] = [];
    let cur: TreeNode | null = root;
    while (stack.length !== 0 || cur !== null) {
        if (cur !== null) {
            stack.push(cur);
            cur = cur.left;
        } else {
            cur = stack.pop();
            res.push(cur.val);
            cur = cur.right;
        }
    }
    return res;
};
```

Postorder traversal (Left-Right-Root):

```typescript
var postorderTraversal = function (root: TreeNode | null): number[] {
    let res: number[] = [];
    if (root === null) return res;
    let stack: TreeNode[] = [root];
    let cur: TreeNode | null = null;
    while (stack.length) {
        cur = stack.pop();
        res.push(cur.val);
        cur.left && stack.push(cur.left);
        cur.right && stack.push(cur.right);
    }
    return res.reverse()
};
```

##### Breadth-First Search (Queue)

```typescript
var levelOrder = function (root: TreeNode | null): number[] {
    let res: number[] = [];
    if (root === null) return res;
    let queue: TreeNode[] = [root];
    while (queue.length) {
        let n: number = queue.length;
        let temp: number[] = [];
        for (let i: number = 0; i < n; i++) {
            let node: TreeNode = queue.shift();
            temp.push(node.val);
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        res.push(temp);
    }
    return res;
};
```

##### Binary Tree Depth

```typescript
var getDepth = function (node: TreNode | null): number {
    if (node === null) return 0;
    return 1 + Math.max(getDepth(node.left), getDepth(node.right));
}
```

##### Binary Tree Node Count

```typescript
var countNodes = function (root: TreeNode | null): number {
    if (root === null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```

#### Backtracking Algorithm 

```typescript
function backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

#### Union-Find 

```typescript
    let n: number = 1005; // Define according to the problem statement 
    let father: number[] = new Array(n).fill(0);

    // Union-Find initialization
    function init () {
        for (int i: number = 0; i < n; ++i) {
            father[i] = i;
        }
    }
    // Find the root in the Union-Find structure
    function find (u: number): number {
        return u === father[u] ? u : father[u] = find(father[u]);
    }
    // Add the edge v->u to the Union-Find
    function join(u: number, v: number) {
        u = find(u);
        v = find(v);
        if (u === v) return ;
        father[v] = u;
    }
    // Check if u and v share the same root
    function same(u: number, v: number): boolean {
        u = find(u);
        v = find(v);
        return u === v;
    }
```

Java：

### Python：

#### Binary Search

```python
def binarysearch(nums, target):
    low = 0
    high = len(nums) - 1
    while (low <= high):
        mid = (high + low)//2

        if (nums[mid] < target):
            low = mid + 1
            
        if (nums[mid] > target):
            high = mid - 1
            
        if (nums[mid] == target):
            return mid

    return -1
```

#### KMP

```python 
def kmp(self, a, s):
    # a: length of the array
    # s: string 
    
    next = [0]*a
    j = 0    
    next[0] = 0
 
    for i in range(1, len(s)):
        while j > 0 and s[j] != s[i]:
            j = next[j - 1]
            
        if s[j] == s[i]:
            j += 1
        next[i] = j
    return next 
```

Go: