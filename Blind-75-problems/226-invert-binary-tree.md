# 226. Invert Binary Tree

Difficulty — Easy

Given the root of a binary tree, invert the tree, and return its root.

## Examples

Example 1:

Input: `root = [4,2,7,1,3,6,9]`  
Output: `[4,7,2,9,6,3,1]`

Example 2:

Input: `root = [2,1,3]`  
Output: `[2,3,1]`

Example 3:

Input: `root = []`  
Output: `[]`

## Constraints

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

---

## Solutions

### 1) Your recursive solution (swap and recurse)
Your solution recursively swaps left and right children, then recurses on both subtrees. Clean and easy to understand.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        // Base case: if root is null, return it (nothing to invert)
        if (root == null) {
            return root;
        }
        
        // Swap left and right children using a temporary variable
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        // Recursively invert the left subtree
        invertTree(root.left);
        
        // Recursively invert the right subtree
        invertTree(root.right);
        
        return root;
    }
}
```

- Time complexity: O(n) — visit each node once
- Space complexity: O(h) recursion stack where h is tree height

### 2) One-liner recursive (compact)
If you want the most concise form, swap and recurse in a single return statement.

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```

- Time complexity: O(n)
- Space complexity: O(h)

### 3) Iterative BFS (using queue)
If you prefer an iterative approach, use a queue to process nodes level-by-level.

```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        
        Deque<TreeNode> queue = new ArrayDeque<>();
        queue.add(root);
        
        while (!queue.isEmpty()) {
            TreeNode node = queue.removeFirst();
            // Swap left and right
            TreeNode temp = node.left;
            node.left = node.right;
            node.right = temp;
            
            // Add children to queue for processing
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        return root;
    }
}
```

- Time complexity: O(n)
- Space complexity: O(n) for the queue

---

## Interview tips

- Start with your recursive approach: swap, then recurse left and right.
- Mention the base case: null nodes return immediately.
- Complexity: O(n) time (visit all nodes), O(h) space (recursion depth).
- If asked for iterative, describe the queue-based level-order traversal.


File: `Blind-75-problems/226-invert-binary-tree.md`