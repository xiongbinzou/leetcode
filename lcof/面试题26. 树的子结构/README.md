# [面试题 26. 树的子结构](https://leetcode.cn/problems/shu-de-zi-jie-gou-lcof/)

## 题目描述

<p>输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)</p>

<p>B是A的子结构， 即 A中有出现和B相同的结构和节点值。</p>

<p>例如:<br>
给定的树 A:</p>

<p><code>&nbsp; &nbsp; &nbsp;3<br>
&nbsp; &nbsp; / \<br>
&nbsp; &nbsp;4 &nbsp; 5<br>
&nbsp; / \<br>
&nbsp;1 &nbsp; 2</code><br>
给定的树 B：</p>

<p><code>&nbsp; &nbsp;4&nbsp;<br>
&nbsp; /<br>
&nbsp;1</code><br>
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>A = [1,2,3], B = [3,1]
<strong>输出：</strong>false
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>A = [3,4,5,1,2], B = [4,1]
<strong>输出：</strong>true</pre>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 节点个数 &lt;= 10000</code></p>

## 解法

<!-- tabs:start -->

### **Python3**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        def dfs(A, B):
            if B is None:
                return True
            if A is None or A.val != B.val:
                return False
            return dfs(A.left, B.left) and dfs(A.right, B.right)

        if A is None or B is None:
            return False
        return dfs(A, B) or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)
```

### **Java**

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if (A == null || B == null) {
            return false;
        }
        return dfs(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }

    private boolean dfs(TreeNode A, TreeNode B) {
        if (B == null) {
            return true;
        }
        if (A == null || A.val != B.val) {
            return false;
        }
        return dfs(A.left, B.left) && dfs(A.right, B.right);
    }
}
```

### **JavaScript**

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} A
 * @param {TreeNode} B
 * @return {boolean}
 */
var isSubStructure = function (A, B) {
    function dfs(A, B) {
        if (!B) return true;
        if (!A || A.val != B.val) return false;
        return dfs(A.left, B.left) && dfs(A.right, B.right);
    }
    if (!A || !B) return false;
    return dfs(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
};
```

### **Go**

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSubStructure(A *TreeNode, B *TreeNode) bool {
	var dfs func(A, B *TreeNode) bool
	dfs = func(A, B *TreeNode) bool {
		if B == nil {
			return true
		}
		if A == nil || A.Val != B.Val {
			return false
		}
		return dfs(A.Left, B.Left) && dfs(A.Right, B.Right)
	}
	if A == nil || B == nil {
		return false
	}
	return dfs(A, B) || isSubStructure(A.Left, B) || isSubStructure(A.Right, B)
}
```

### **C++**

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
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if (!A || !B) return 0;
        return dfs(A, B) || isSubStructure(A->left, B) || isSubStructure(A->right, B);
    }

    bool dfs(TreeNode* A, TreeNode* B) {
        if (!B) return 1;
        if (!A || A->val != B->val) return 0;
        return dfs(A->left, B->left) && dfs(A->right, B->right);
    }
};
```

### **TypeScript**

```ts
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isSubStructure(A: TreeNode | null, B: TreeNode | null): boolean {
    if (A == null || B == null) {
        return false;
    }
    return dfs(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
}

function dfs(A: TreeNode | null, B: TreeNode | null) {
    if (B == null) {
        return true;
    }
    if (A == null) {
        return false;
    }
    return A.val === B.val && dfs(A.left, B.left) && dfs(A.right, B.right);
}
```

### **Rust**

```rust
// Definition for a binary tree node.
// #[derive(Debug, PartialEq, Eq)]
// pub struct TreeNode {
//   pub val: i32,
//   pub left: Option<Rc<RefCell<TreeNode>>>,
//   pub right: Option<Rc<RefCell<TreeNode>>>,
// }
//
// impl TreeNode {
//   #[inline]
//   pub fn new(val: i32) -> Self {
//     TreeNode {
//       val,
//       left: None,
//       right: None
//     }
//   }
// }
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn is_sub_structure(
        a: Option<Rc<RefCell<TreeNode>>>,
        b: Option<Rc<RefCell<TreeNode>>>,
    ) -> bool {
        Self::is_sub_structure_help(&a, &b)
    }

    fn is_sub_structure_help(
        a: &Option<Rc<RefCell<TreeNode>>>,
        b: &Option<Rc<RefCell<TreeNode>>>,
    ) -> bool {
        if a.is_none() || b.is_none() {
            return false;
        }

        Self::dfs(a, b)
            || Self::is_sub_structure_help(&a.as_ref().unwrap().borrow().left, b)
            || Self::is_sub_structure_help(&a.as_ref().unwrap().borrow().right, b)
    }

    fn dfs(a: &Option<Rc<RefCell<TreeNode>>>, b: &Option<Rc<RefCell<TreeNode>>>) -> bool {
        if b.is_none() {
            return true;
        }
        if a.is_none() {
            return false;
        }
        let a = a.as_ref().unwrap().borrow();
        let b = b.as_ref().unwrap().borrow();
        a.val == b.val && Self::dfs(&a.left, &b.left) && Self::dfs(&a.right, &b.right)
    }
}
```

### **C#**

```cs
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public bool IsSubStructure(TreeNode A, TreeNode B) {
        if (A == null || B == null) {
            return false;
        }
        return dfs(A, B) || IsSubStructure(A.left, B) || IsSubStructure(A.right, B);
    } 

    public bool dfs(TreeNode A, TreeNode B) {
        if (B == null) {
            return true;
        }
        if (A == null || A.val != B.val) {
            return false;
        }
        return dfs(A.left, B.left) && dfs(A.right, B.right);
    }
}
```

### **...**

```

```

<!-- tabs:end -->
