# Recursive Traversal of Binary Trees

## Thought Process

This time, let's have a thorough discussion on recursion. Many students find recursive algorithms to be something they "understand at first glance but fail to write".

This is primarily due to a lack of systematic understanding and methodology of recursion — each time they write a recursive algorithm, they rely on an almost mystical intuition rather than a structured approach. As a result, whether their code passes or not often feels like leaving things to chance.

In this article, we will introduce the recursive methods for preorder, inorder, and postorder traversal. Some might find this simple, but the truth is that we need to establish a methodical approach through these straightforward problems. With a solid methodology, we can then tackle more complex recursive problems.

Here, we'll help you establish the three key elements of recursive algorithms. Every time you write a recursive function, follow these three elements to ensure you write a correct recursive algorithm!

1. **Identify the parameters and return type of the recursive function:**
   Determine which parameters need to be dealt with during recursion, and include them in the recursive function if necessary. Additionally, clarify the return value of each recursive call to decide on the return type of the function.

2. **Determine the termination condition:**
   After writing the recursive algorithm, a common error during execution is a stack overflow, which occurs when the termination condition is either missing or incorrect. The operating system uses a stack to store information for each recursive layer. If recursion doesn’t terminate, the memory stack will inevitably overflow.

3. **Define the logic for a single layer of recursion:**
   Determine the information required for each layer of recursion. Within this part, you'll typically make further recursive calls, thus implementing the recursive process.

Now that we have confirmed these three elements, let's put them into practice:

**Let's take preorder traversal as an example:**

1. **Identify the recursive function's parameters and return type:** Since we want to print out the values of nodes in preorder traversal, we need to pass a vector to store the node values. Other than this, there isn't additional data to process, nor is there a need for a return value. Hence, the return type of the recursive function is `void`. The code structure is as follows:

   ```cpp
   void traversal(TreeNode* cur, vector<int>& vec)
   ```

2. **Determine the termination condition:** During recursion, how do we determine when it should stop? It should end when there's no node to traverse, meaning when the current node is `null`, we directly return:

   ```cpp
   if (cur == NULL) return;
   ```

3. **Define the logic for a single layer of recursion:** Preorder traversal follows the order of "node-left-right", so for a single layer of recursion, we start by recording the node value:

   ```cpp
   vec.push_back(cur->val);    // Node
   traversal(cur->left, vec);  // Left
   traversal(cur->right, vec); // right
   ```

Executing these steps completes the basic preorder traversal algorithm. Here is the complete code:

Preorder Traversal:

```cpp
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& vec) {
        if (cur == NULL) return;
        vec.push_back(cur->val);    // Node
        traversal(cur->left, vec);  // Left
        traversal(cur->right, vec); // Right
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```

After writing the preorder traversal, understanding inorder and postorder traversal isn't difficult. Here is the code:

Inorder Traversal:

```cpp
void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    traversal(cur->left, vec);  // Left
    vec.push_back(cur->val);    // Node
    traversal(cur->right, vec); // Right
}
```

Postorder Traversal:

```cpp
void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    traversal(cur->left, vec);  // Left
    traversal(cur->right, vec); // Right
    vec.push_back(cur->val);    // Node
}
```

At this point, you can try solving the following LeetCode problems:

* [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
* [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
* [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Some might find recursive traversal straightforward and wish to explore iterative methods. Don't worry; we'll thoroughly examine iterative methods tomorrow!

## Other Language Versions

### Java:

```Java
// Preorder Traversal - Recursive - LC144_Binary Tree Preorder Traversal
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result) {
        if (root == null) {
            return;
        }
        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
// Inorder Traversal - Recursive - LC94_Binary Tree Inorder Traversal
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }

    void inorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        inorder(root.left, list);
        list.add(root.val);             // Note this line
        inorder(root.right, list);
    }
}
// Postorder Traversal - Recursive - LC145_Binary Tree Postorder Traversal
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorder(root, res);
        return res;
    }

    void postorder(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        postorder(root.left, list);
        postorder(root.right, list);
        list.add(root.val);             // Note this line
    }
}
```

### Python:

```python
# Preorder Traversal - Recursive - LC144_Binary Tree Preorder Traversal
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        
        def dfs(node):
            if node is None:
                return
            
            res.append(node.val)
            dfs(node.left)
            dfs(node.right)
        dfs(root)
        return res

```
```python
# Inorder Traversal - Recursive - LC94_Binary Tree Inorder Traversal
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        
        def dfs(node):
            if node is None:
                return
            
            dfs(node.left)
            res.append(node.val)
            dfs(node.right)
        dfs(root)
        return res
```
```python


# Postorder Traversal - Recursive - LC145_Binary Tree Postorder Traversal
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        
        def dfs(node):
            if node is None:
                return
            
            dfs(node.left)
            dfs(node.right)
            res.append(node.val)

        dfs(root)
        return res
```

### Go:

Preorder Traversal:
```go
func preorderTraversal(root *TreeNode) (res []int) {
    var traversal func(node *TreeNode)
    traversal = func(node *TreeNode) {
	if node == nil {
            return
	}
	res = append(res,node.Val)
	traversal(node.Left)
	traversal(node.Right)
    }
    traversal(root)
    return res
}

```
Inorder Traversal:

```go
func inorderTraversal(root *TreeNode) (res []int) {
    var traversal func(node *TreeNode)
    traversal = func(node *TreeNode) {
	if node == nil {
	    return
	}
	traversal(node.Left)
	res = append(res,node.Val)
	traversal(node.Right)
    }
    traversal(root)
    return res
}
```
Postorder Traversal:

```go
func postorderTraversal(root *TreeNode) (res []int) {
    var traversal func(node *TreeNode)
    traversal = func(node *TreeNode) {
	if node == nil {
	    return
	}
	traversal(node.Left)
	traversal(node.Right)
        res = append(res,node.Val)
    }
    traversal(root)
    return res
}
```

### JavaScript:

Preorder Traversal:
```Javascript
var preorderTraversal = function(root) {
// Method 1
//  let res=[];
//  const dfs=function(root){
//      if(root===null)return ;
//      // Start with the parent node since it's preorder
//      res.push(root.val);
//      // Recur on the left subtree
//      dfs(root.left);
//      // Recur on the right subtree
//      dfs(root.right);
//  }
//  // Use a closure to store the result with only one parameter
//  dfs(root);
//  return res;
// Method 2
  return root
    ? [
        // Preorder: Node, Left, Right
        root.val,
        // Recur on the left subtree
        ...preorderTraversal(root.left),
        // Recur on the right subtree
        ...preorderTraversal(root.right),
      ]
    : [];
};
```
Inorder Traversal
```javascript
var inorderTraversal = function(root) {
// Method 1

    // let res=[];
    // const dfs=function(root){
    //     if(root===null){
    //         return ;
    //     }
    //     dfs(root.left);
    //     res.push(root.val);
    //     dfs(root.right);
    // }
    // dfs(root);
    // return res;

// Method 2
  return root
    ? [
        // Inorder: Left, Node, Right
        // Recur on the left subtree
        ...inorderTraversal(root.left),
        root.val,
        // Recur on the right subtree
        ...inorderTraversal(root.right),
      ]
    : [];
};
```

Postorder Traversal
```javascript
var postorderTraversal = function(root) {
    // Method 1
    // let res=[];
    // const dfs=function(root){
    //     if(root===null){
    //         return ;
    //     }
    //     dfs(root.left);
    //     dfs(root.right);
    //     res.push(root.val);
    // }
    // dfs(root);
    // return res;

  // Method 2
  // Postorder: Left, Right, Node
  return root
    ? [
        // Recur on the left subtree
        ...postorderTraversal(root.left),
        // Recur on the right subtree
        ...postorderTraversal(root.right),
        root.val,
      ]
    : [];
};
```

### TypeScript:

```typescript
// Preorder Traversal
function preorderTraversal(node: TreeNode | null): number[] {
    function traverse(node: TreeNode | null, res: number[]): void {
        if (node === null) return;
        res.push(node.val);
        traverse(node.left, res);
        traverse(node.right, res);
    }
    const res: number[] = [];
    traverse(node, res);
    return res;
}

// Inorder Traversal
function inorderTraversal(node: TreeNode | null): number[] {
    function traverse(node: TreeNode | null, res: number[]): void {
        if (node === null) return;
        traverse(node.left, res);
        res.push(node.val);
        traverse(node.right, res);
    }
    const res: number[] = [];
    traverse(node, res);
    return res;
}

// Postorder Traversal
function postorderTraversal(node: TreeNode | null): number[] {
    function traverse(node: TreeNode | null, res: number[]): void {
        if (node === null) return;
        traverse(node.left, res);
        traverse(node.right, res);
        res.push(node.val);
    }
    const res: number[] = [];
    traverse(node, res);
    return res;
}
```

### C:

```c
//Preorder Traversal:
void preOrder(struct TreeNode* root, int* ret, int* returnSize) {
    if(root == NULL)
        return;
    ret[(*returnSize)++] = root->val;
    preOrder(root->left, ret, returnSize);
    preOrder(root->right, ret, returnSize);
}

int* preorderTraversal(struct TreeNode* root, int* returnSize){
    int* ret = (int*)malloc(sizeof(int) * 100);
    *returnSize = 0;
    preOrder(root, ret, returnSize);
    return ret;
}

//Inorder Traversal:
void inOrder(struct TreeNode* node, int* ret, int* returnSize) {
    if(!node)
        return;
    inOrder(node->left, ret, returnSize);
    ret[(*returnSize)++] = node->val;
    inOrder(node->right, ret, returnSize);
}

int* inorderTraversal(struct TreeNode* root, int* returnSize){
    int* ret = (int*)malloc(sizeof(int) * 100);
    *returnSize = 0;
    inOrder(root, ret, returnSize);
    return ret;
}

//Postorder Traversal:
void postOrder(struct TreeNode* node, int* ret, int* returnSize) {
    if(node == NULL) 
        return;
    postOrder(node->left, ret, returnSize);
    postOrder(node->right, ret, returnSize);
    ret[(*returnSize)++] = node->val;
}

int* postorderTraversal(struct TreeNode* root, int* returnSize){
    int* ret= (int*)malloc(sizeof(int) * 100);
    *returnSize = 0;
    postOrder(root, ret, returnSize);
    return ret;
}
```

### Swift:
Preorder Traversal: (LC144_Binary Tree Preorder Traversal)

```Swift
func preorderTraversal(_ root: TreeNode?) -> [Int] {
    var res = [Int]()
    preorder(root, res: &res)
    return res
}
func preorder(_ root: TreeNode?, res: inout [Int]) {
    if root == nil {
        return
    }
    res.append(root!.val)
    preorder(root!.left, res: &res)
    preorder(root!.right, res: &res)
}
```

Inorder Traversal: (LC94_Binary Tree Inorder Traversal)
```Swift
func inorderTraversal(_ root: TreeNode?) -> [Int] {
    var res = [Int]()
    inorder(root, res: &res)
    return res
}
func inorder(_ root: TreeNode?, res: inout [Int]) {
    if root == nil {
        return
    }
    inorder(root!.left, res: &res)
    res.append(root!.val)
    inorder(root!.right, res: &res)
}
```

Postorder Traversal: (LC145_Binary Tree Postorder Traversal)
```Swift
func postorderTraversal(_ root: TreeNode?) -> [Int] {
    var res = [Int]()
    postorder(root, res: &res)
    return res
}
func postorder(_ root: TreeNode?, res: inout [Int]) {
    if root == nil {
        return
    }
    postorder(root!.left, res: &res)
    postorder(root!.right, res: &res)
    res.append(root!.val)
}
```
### Scala:

 Preorder Traversal: (LC144_Binary Tree Preorder Traversal)

```scala
object Solution {
  import scala.collection.mutable.ListBuffer
  def preorderTraversal(root: TreeNode): List[Int] = {
    val res = ListBuffer[Int]()
    def traversal(curNode: TreeNode): Unit = {
      if(curNode == null) return
      res.append(curNode.value)
      traversal(curNode.left)
      traversal(curNode.right)
    }
    traversal(root)
    res.toList
  }
}
```
Inorder Traversal: (LC94_Binary Tree Inorder Traversal)
```scala
object Solution {  
  import scala.collection.mutable.ListBuffer
  def inorderTraversal(root: TreeNode): List[Int] = {
    val res = ListBuffer[Int]()
    def traversal(curNode: TreeNode): Unit = {
      if(curNode == null) return
      traversal(curNode.left)
      res.append(curNode.value)
      traversal(curNode.right)
    }
    traversal(root)
    res.toList
  }
}
```
Postorder Traversal: (LC145_Binary Tree Postorder Traversal)
```scala
object Solution {
  import scala.collection.mutable.ListBuffer
  def postorderTraversal(root: TreeNode): List[Int] = {
    val res = ListBuffer[Int]()
    def traversal(curNode: TreeNode): Unit = {
      if (curNode == null) return
      traversal(curNode.left)
      traversal(curNode.right)
      res.append(curNode.value)
    }
    traversal(root)
    res.toList
  }
}
```

### Rust:

```rust
use std::cell::RefCell;
use std::rc::Rc;
impl Solution {
    pub fn preorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut res = vec![];
        Self::traverse(&root, &mut res);
        res
    }

//Preorder Traversal
    pub fn traverse(root: &Option<Rc<RefCell<TreeNode>>>, res: &mut Vec<i32>) {
        if let Some(node) = root {
            res.push(node.borrow().val);
            Self::traverse(&node.borrow().left, res);
            Self::traverse(&node.borrow().right, res);
        }
    }
//Postorder Traversal
    pub fn traverse(root: &Option<Rc<RefCell<TreeNode>>>, res: &mut Vec<i32>) {
        if let Some(node) = root {
            Self::traverse(&node.borrow().left, res);
            Self::traverse(&node.borrow().right, res);
            res.push(node.borrow().val);
        }
    }
//Inorder Traversal
    pub fn traverse(root: &Option<Rc<RefCell<TreeNode>>>, res: &mut Vec<i32>) {
        if let Some(node) = root {
            Self::traverse(&node.borrow().left, res);
            res.push(node.borrow().val);
            Self::traverse(&node.borrow().right, res);
        }
    }
}
```

### C#
```csharp
// Preorder Traversal
public IList<int> PreorderTraversal(TreeNode root)
{
    var res = new List<int>();
    if (root == null) return res;
    Traversal(root, res);
    return res;

}
public void Traversal(TreeNode cur, IList<int> res)
{
    if (cur == null) return;
    res.Add(cur.val);
    Traversal(cur.left, res);
    Traversal(cur.right, res);
}
```
```csharp
// Inorder Traversal
public IList<int> InorderTraversal(TreeNode root)
{
    var res = new List<int>();
    if (root == null) return res;
    Traversal(root, res);
    return res;
}
public void Traversal(TreeNode cur, IList<int> res)
{
    if (cur == null) return;
    Traversal(cur.left, res);
    res.Add(cur.val);
    Traversal(cur.right, res);
}
```
```csharp
// Postorder Traversal
public IList<int> PostorderTraversal(TreeNode root)
{
    var res = new List<int>();
    if (root == null) return res;
    Traversal(root, res);
    return res;
}
public void Traversal(TreeNode cur, IList<int> res)
{
    if (cur == null) return;
    Traversal(cur.left, res);
    Traversal(cur.right, res);
    res.Add(cur.val);
}
```

### PHP
```php
// LC144 - Preorder Traversal
function preorderTraversal($root) {
    $output = [];
    $this->traversal($root, $output);
    return $output;
}

function traversal($root, array &$output) {
    if ($root->val === null) {
        return;
    }

    $output[] = $root->val;
    $this->traversal($root->left, $output);
    $this->traversal($root->right, $output);
}
```
```php
// LC94 - Inorder Traversal
function inorderTraversal($root) {
    $output = [];
    $this->traversal($root, $output);
    return $output;
}

function traversal($root, array &$output) {
    if ($root->val === null) {
        return;
    }

    $this->traversal($root->left, $output);
    $output[] = $root->val;
    $this->traversal($root->right, $output);
}
```
```php
// LC145 - Postorder Traversal
function postorderTraversal($root) {
    $output = [];
    $this->traversal($root, $output);
    return $output;
}

function traversal($root, array &$output) {
    if ($root->val === null) {
        return;
    }

    $this->traversal($root->left, $output);
    $this->traversal($root->right, $output);
    $output[] = $root->val;
}
```