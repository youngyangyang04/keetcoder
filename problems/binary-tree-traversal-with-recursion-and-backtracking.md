# Binary Tree: Even Though Using Recursion, There Is Backtracking Hidden

> Add an explanation

In yesterday's summary [Still Playing? It's Time to Summarize! (Weekly Summary: Binary Tree)](https://keetcoder.com/problems/周总结/20201003二叉树周末总结.html), there are two points that need further clarification.

## Check Identical Trees

In [Still Playing? It's Time to Summarize! (Weekly Summary: Binary Tree)](https://keetcoder.com/problems/周总结/20201003二叉树周末总结.html), I mistakenly posted the code for checking symmetric trees when explaining the code for Problem 100. Identical Trees. Attentive readers should have noticed this mistake.

So here, I'll provide the correct code for Problem 100. Identical Trees:

```cpp
class Solution {
public:
    bool compare(TreeNode* tree1, TreeNode* tree2) {
        if (tree1 == NULL && tree2 != NULL) return false;
        else if (tree1 != NULL && tree2 == NULL) return false;
        else if (tree1 == NULL && tree2 == NULL) return true;
        else if (tree1->val != tree2->val) return false; // Note: I didn't use else here

        // At this point: both nodes are non-null and have the same value
        // Only then proceed with the recursive check for the next level
        bool compareLeft = compare(tree1->left, tree2->left);       // Left subtree: left, Right subtree: left
        bool compareRight = compare(tree1->right, tree2->right);    // Left subtree: right, Right subtree: right
        bool isSame = compareLeft && compareRight;                  // Left subtree: middle, Right subtree: middle (logical check)
        return isSame;
    }
    bool isSameTree(TreeNode* p, TreeNode* q) {
        return compare(p, q);
    }
};
```

The above code, compared to [Binary Tree: Am I Symmetrical?](https://keetcoder.com/problems/0101.symmetric-tree.html), only changes some variable names (to match the context of checking identical trees) and the order of traversal.

You should realize that after understanding the [essence of checking symmetric trees](https://keetcoder.com/problems/0101.symmetric-tree.html), the code for symmetric trees can be slightly modified and directly used to solve Problem 100. Identical Trees.

## Backtracking Hidden in Recursion

In [Binary Tree: Find All My Paths?](https://keetcoder.com/problems/0257.binary-tree-paths.html), I emphasized that this problem actually involves backtracking and provided the first version of code which fully demonstrates the backtracking process.

Here is the code that fully demonstrates backtracking: (257. Binary Tree Paths)

```cpp
class Solution {
private:
    void traversal(TreeNode* cur, vector<int>& path, vector<string>& result) {
        path.push_back(cur->val);
        // Now we've reached a leaf node
        if (cur->left == NULL && cur->right == NULL) {
            string sPath;
            for (int i = 0; i < path.size() - 1; i++) {
                sPath += to_string(path[i]);
                sPath += "->";
            }
            sPath += to_string(path[path.size() - 1]);
            result.push_back(sPath);
            return;
        }
        if (cur->left) {
            traversal(cur->left, path, result);
            path.pop_back(); // Backtrack
        }
        if (cur->right) {
            traversal(cur->right, path, result);
            path.pop_back(); // Backtrack
        }
    }

public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        vector<int> path;
        if (root == NULL) return result;
        traversal(root, path, result);
        return result;
    }
};
```

Here is the more concise recursive code: (257. Binary Tree Paths)

```cpp
class Solution {
private:
    void traversal(TreeNode* cur, string path, vector<string>& result) {
        path += to_string(cur->val); // Middle
        if (cur->left == NULL && cur->right == NULL) {
            result.push_back(path);
            return;
        }
        if (cur->left) traversal(cur->left, path + "->", result); // Left: Backtracking is hidden here
        if (cur->right) traversal(cur->right, path + "->", result); // Right: Backtracking is hidden here
    }

public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> result;
        string path;
        if (root == NULL) return result;
        traversal(root, path, result);
        return result;
    }
};
```

In the code above, backtracking seems invisible. Yet, backtracking is hidden in `traversal(cur->left, path + "->", result);` using `path + "->"`. Each time the function is called, `path` remains unchanged, which is equivalent to backtracking.

To illustrate the backtracking process in this concise code, you can try replacing:

```cpp
if (cur->left) traversal(cur->left, path + "->", result); // Left: backtracking is hidden here
```

with:

```cpp
path += "->";
traversal(cur->left, path, result); // Left
```

That is:

```cpp
if (cur->left) {
    path += "->";
    traversal(cur->left, path, result); // Left
}
if (cur->right) {
    path += "->";
    traversal(cur->right, path, result); // Right
}
```

Since we need to restore `path` before traversing the right subtree, backtracking is necessary after the left subtree traversal. Although technically unnecessary in the concise code, adding it allows for successful AC.

```cpp
if (cur->left) {
    path += "->";
    traversal(cur->left, path, result); // Left
    path.pop_back(); // Backtrack: Remove val
    path.pop_back(); // Backtrack: Remove "->"
}
if (cur->right) {
    path += "->";
    traversal(cur->right, path, result); // Right
    path.pop_back(); // Backtrack (Not required)
    path.pop_back(); 
}
```

You should realize that using `path + "->"` as a function parameter works because `path` remains unchanged after the recursion function finishes, giving the equivalent of backtracking.

If you've forgotten some details, I suggest revisiting [Binary Tree: Find All My Paths?](https://keetcoder.com/problems/0257.binary-tree-paths.html) before reading this summary again—I'm confident you'll find clarity.

I have tried to unearth every logical detail here, and I hope it helps!

## Versions in Other Languages

### Java:

100. Identical Trees: Recursive Code

```java
class Solution {
    public boolean compare(TreeNode tree1, TreeNode tree2) {
       
        if(tree1==null && tree2==null)return true;
        if(tree1==null || tree2==null)return false;
        if(tree1.val!=tree2.val)return false;
        // Both subtrees are non-null and have the same value
        // Now perform the recursive check for the next level
        boolean compareLeft = compare(tree1.left, tree2.left);       // Left subtree: left, Right subtree: left
        boolean compareRight = compare(tree1.right, tree2.right);    // Left subtree: right, Right subtree: right
        boolean isSame = compareLeft && compareRight;                  // Left subtree: middle, Right subtree: middle (logical process)
        return isSame;

    }
    boolean isSameTree(TreeNode p, TreeNode q) {
        return compare(p, q);
    }
}
```

257. Binary Tree Paths: Backtracking Code

```java
class Solution {
    public void traversal(TreeNode cur, List<Integer> path, List<String> result) {
        path.add(cur.val);
        // Reached a leaf node
        if (cur.left == null && cur.right == null) {
            String sPath = "";
            for (int i = 0; i < path.size() - 1; i++) {
                sPath += "" + path.get(i);
                sPath += "->";
            }
            sPath += path.get(path.size() - 1);
            result.add(sPath);
            return;
        }
        if (cur.left != null) {
            traversal(cur.left, path, result);
            path.remove(path.size() - 1); // Backtrack
        }
        if (cur.right != null) {
            traversal(cur.right, path, result);
            path.remove(path.size() - 1); // Backtrack
        }
    }
    
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new LinkedList<>();
        List<Integer> path = new LinkedList<>();
        if (root == null) return result;
        traversal(root, path, result);
        return result;
    }
}
```

Refined recursive code (257. Binary Tree Paths):

```java
class Solution {
    public void traversal(TreeNode cur, String path, List<String> result) {
        path += cur.val; // Middle
        if (cur.left == null && cur.right == null) {
            result.add(path);
            return;
        }
        if (cur.left != null) traversal(cur.left, path + "->", result); // Left: Backtracking is hidden here
        if (cur.right != null) traversal(cur.right, path + "->", result); // Right: Backtracking is hidden here
    }

    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new LinkedList<>();
        String path = "";
        if (root == null) return result;
        traversal(root, path, result);
        return result;
    }
}
```

### Python:

100. Identical Trees
> Recursive Method

```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        return self.compare(p, q)
        
    def compare(self, tree1, tree2):
        if not tree1 and tree2:
            return False
        elif tree1 and not tree2:
            return False
        elif not tree1 and not tree2:
            return True
        elif tree1.val != tree2.val: # Notice I didn't use else here
            return False
        
        # At this point: both nodes are not null and values are equal
        # Perform recursion for next-level checks
        compareLeft = self.compare(tree1.left, tree2.left) # Left subtree: left, Right sub: left
        compareRight = self.compare(tree1.right, tree2.right) # Left subtree: right, Right sub: right
        isSame = compareLeft and compareRight # Left subtree: middle, Right sub: middle (logical check)
        return isSame
```

257. Binary Tree Paths
> Backtracking Hidden in Recursion

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        result = []
        path = []
        if not root:
            return result
        self.traversal(root, path, result)
        return result
        
    def traversal(self, cur, path, result):
        path.append(cur.val)
        # At leaf node
        if not cur.left and not cur.right:
            sPath = ""
            for i in range(len(path)-1):
                sPath += str(path[i])
                sPath += "->"
            sPath += str(path[len(path)-1])
            result.append(sPath)
            return
        if cur.left:
            self.traversal(cur.left, path, result)
            path.pop() # Backtrack
        if cur.right:
            self.traversal(cur.right, path, result)
            path.pop() # Backtrack
```

> Refined version

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        result = []
        path = ""
        if not root:
            return result
        self.traversal(root, path, result)
        return result
        
    def traversal(self, cur, path, result):
        path += str(cur.val) # Middle
        if not cur.left and not cur.right:
            result.append(path)
            return
        if cur.left:
            self.traversal(cur.left, path+"->", result) # Left: backtracking hidden
        if cur.right:
            self.traversal(cur.right, path+"->", result) # Right: backtracking hidden
```

### Go:

100. Identical Trees
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSameTree(p *TreeNode, q *TreeNode) bool {
    switch {
    case p == nil && q == nil:
        return true
    case p == nil || q == nil:
        fallthrough
    case p.Val != q.Val:
        return false
    }
    return isSameTree(p.Left, q.Left) && isSameTree(p.Right, q.Right)
}
```

257. Binary Tree Paths
> Recursive Method

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func binaryTreePaths(root *TreeNode) []string {
    var result []string
    traversal(root, &result, "")
    return result
}
func traversal(root *TreeNode, result *[]string, pathStr string) {
    if len(pathStr) != 0 {
        pathStr = pathStr + "->" + strconv.Itoa(root.Val)
    } else {
        pathStr = strconv.Itoa(root.Val)
    }
    if root.Left == nil && root.Right == nil {
        *result = append(*result, pathStr)
        return 
    }
    if root.Left != nil {
        traversal(root.Left, result, pathStr)
    }
    if root.Right != nil {
        traversal(root.Right, result, pathStr)
    }
}
```

> Backtracking Method

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func binaryTreePaths(root *TreeNode) []string {
    var result []string
    var path []int
    traversal(root, &result, &path)
    return result
}
func traversal(root *TreeNode, result *[]string, path *[]int) {
    *path = append(*path, root.Val)
    if root.Left == nil && root.Right == nil {
        pathStr := strconv.Itoa((*path)[0])
        for i := 1; i < len(*path); i++ {
            pathStr = pathStr + "->" + strconv.Itoa((*path)[i])
        }
        *result = append(*result, pathStr)
        return 
    }
    if root.Left != nil {
        traversal(root.Left, result, path)
        *path = (*path)[:len(*path)-1] // Backtrack
    }
    if root.Right != nil {
        traversal(root.Right, result, path)
        *path = (*path)[:len(*path)-1] // Backtrack
    }
}
```

### JavaScript:

100. Identical Trees
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val === undefined ? 0 : val)
 *     this.left = (left === undefined ? null : left)
 *     this.right = (right === undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if (p === null && q === null) {
        return true;
    } else if (p === null || q === null) {
        return false;
    } else if (p.val !== q.val) {
        return false;
    } else {
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
};
```

257. Binary Tree Paths

> Backtracking Method:

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val === undefined ? 0 : val)
 *     this.left = (left === undefined ? null : left)
 *     this.right = (right === undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {string[]}
 */
var binaryTreePaths = function(root) {
    const getPath = (root, path, result) => {
        path.push(root.val);
        if (root.left === null && root.right === null) {
            let n = path.length;
            let str = '';
            for (let i = 0; i < n - 1; i++) {
                str += path[i] + '->';
            }
            str += path[n - 1];
            result.push(str);
        }

        if (root.left !== null) {
            getPath(root.left, path, result);
            path.pop();   // Backtrack
        }

        if (root.right !== null) {
            getPath(root.right, path, result);
            path.pop(); 
        }
    }
    
    if (root === null) return [];
    let result = [];
    let path = [];
    getPath(root, path, result);
    return result;
};
```

### TypeScript:

> Identical Trees

```typescript
function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (p === null && q === null) return true;
    if (p === null || q === null) return false;
    if (p.val !== q.val) return false;
    let bool1: boolean, bool2: boolean;
    bool1 = isSameTree(p.left, q.left);
    bool2 = isSameTree(p.right, q.right);
    return bool1 && bool2;
};
```

> Binary Tree Paths

```typescript
function binaryTreePaths(root: TreeNode | null): string[] {
    function recur(node: TreeNode, nodeSeqArr: number[], resArr: string[]): void {
        nodeSeqArr.push(node.val);
        if (node.left === null && node.right === null) {
            resArr.push(nodeSeqArr.join('->'));
        }
        if (node.left !== null) {
            recur(node.left, nodeSeqArr, resArr);
            nodeSeqArr.pop();
        }
        if (node.right !== null) {
            recur(node.right, nodeSeqArr, resArr);
            nodeSeqArr.pop();
        }
    }
    let nodeSeqArr: number[] = [];
    let resArr: string[] = [];
    if (root === null) return resArr;
    recur(root, nodeSeqArr, resArr);
    return resArr;
};
```

### Swift:
> Identical Trees
```swift
// Recursive
func isSameTree(_ p: TreeNode?, _ q: TreeNode?) -> Bool {
    return _isSameTree3(p, q)
}
func _isSameTree3(_ p: TreeNode?, _ q: TreeNode?) -> Bool {
    if p == nil && q == nil {
        return true
    } else if p == nil && q != nil {
        return false
    } else if p != nil && q == nil {
        return false
    } else if p!.val != q!.val {
        return false
    }
    let leftSide = _isSameTree3(p!.left, q!.left)
    let rightSide = _isSameTree3(p!.right, q!.right)
    return leftSide && rightSide
}
```

> Binary Tree Paths
```swift
// Recursive/Backtracking
func binaryTreePaths(_ root: TreeNode?) -> [String] {
    var res = [String]()
    guard let root = root else {
        return res
    }
    var paths = [Int]()
    _binaryTreePaths3(root, res: &res, paths: &paths)
    return res
}
func _binaryTreePaths3(_ root: TreeNode, res: inout [String], paths: inout [Int]) {
    paths.append(root.val)
    if root.left == nil && root.right == nil {
        var str = ""
        for i in 0 ..< (paths.count - 1) {
            str.append("\(paths[i])->")
        }
        str.append("\(paths.last!)")
        res.append(str)
    }
    if let left = root.left {
        _binaryTreePaths3(left, res: &res, paths: &paths)
        paths.removeLast()
    }
    if let right = root.right {
        _binaryTreePaths3(right, res: &res, paths: &paths)
        paths.removeLast()
    }
}
```

### Rust

> Identical Trees

```rust
use std::cell::RefCell;
use std::rc::Rc;
impl Solution {
    pub fn is_same_tree(
        p: Option<Rc<RefCell<TreeNode>>>,
        q: Option<Rc<RefCell<TreeNode>>>,
    ) -> bool {
        match (p, q) {
            (None, None) => true,
            (None, Some(_)) => false,
            (Some(_), None) => false,
            (Some(n1), Some(n2)) => {
                if n1.borrow().val == n2.borrow().val {
                    let right =
                        Self::is_same_tree(n1.borrow().left.clone(), n2.borrow().left.clone());
                    let left =
                        Self::is_same_tree(n1.borrow().right.clone(), n2.borrow().right.clone());
                    right && left
                } else {
                    false
                }
            }
        }
    }
}
```

> Binary Tree Paths

```rust
// Recursive
use std::cell::RefCell;
use std::rc::Rc;
impl Solution {
    pub fn binary_tree_paths(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<String> {
        let mut res = vec![];
        let mut path = vec![];
        Self::recur(&root, &mut path, &mut res);
        res
    }

    pub fn recur(
        root: &Option<Rc<RefCell<TreeNode>>>,
        path: &mut Vec<String>,
        res: &mut Vec<String>,
    ) {
        let node = root.as_ref().unwrap().borrow();
        path.push(node.val.to_string());
        if node.left.is_none() && node.right.is_none() {
            res.push(path.join("->"));
            return;
        }
        if node.left.is_some() {
            Self::recur(&node.left, path, res);
            path.pop(); // Backtrack
        }
        if node.right.is_some() {
            Self::recur(&node.right, path, res);
            path.pop(); // Backtrack
        }
    }
}
```