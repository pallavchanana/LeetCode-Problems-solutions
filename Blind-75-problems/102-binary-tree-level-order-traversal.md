### 102. Binary Tree Level Order Traversal - `Medium`

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

 

Example 1:
Input: root = `[3,9,20,null,null,15,7]`
Output: `[[3],[9,20],[15,7]]`

Example 2:
Input: root = `[1]`
Output: `[[1]]`

Example 3:
Input: root =` []`
Output: `[]`
 

Constraints:

The number of nodes in the tree is in the range `[0, 2000].
-1000 <= Node.val <= 1000`

## Solution

### Pattern  Used
- DFS with level tracking (recursive level‑order).​
Idea: Do a normal DFS, but carry a level parameter and use List<List<T>> so each depth gets its own inner list.

``` java
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        traverse(root, 0, result);
        return result;
    }

    public void traverse(TreeNode node, int level, List<List<Integer>> result) {
        if (node == null) {
            return;
        }
        if (level == result.size()) {
            result.add(new ArrayList<>());
        }
        result.get(level).add(node.val);
        traverse(node.left, level + 1, result);
        traverse(node.right, level + 1, result);
    }
}
```

### Time and Space 
- Time complexity
Each node is enqueued once and dequeued once in BFS, or visited once in DFS, and each visit does only constant‑time work (check children, add to list, etc.).
So total work is proportional to the number of nodes: time complexity 
`O(n)`
​
- Space complexity
The queue (BFS) or recursion stack (DFS) plus the result list together can hold up to all nodes in the tree in the worst case.
Since output itself stores all node values, space complexity is `O(n)` cannot be better than this because of the required output

## Mind Example
```
Step‑by‑step example
Consider tree:
[3,9,20,null,null,15,7] (the LeetCode example).

Traversal order with levels (assuming level starts at 0):

Visit 3 at level 0
result.size() == 0, so create list for level 0: result = [ [] ]
result.get(0).add(3); → result = [ [3] ]
​

Visit 9 at level 1
result.size() == 1, so create list for level 1: result = [ [3], [] ]
result.get(1).add(9); → result = [ [3], [9] ]
​

Visit 20 at level 1
List for level 1 already exists: [9]
result.get(1).add(20); → result = [ [3], [9, 20] ]
​

Visit 15 at level 2
result.size() == 2, so create list for level 2: result = [ [3], [9, 20], [] ]
result.get(2).add(15); → result = [ [3], [9, 20], [15] ]
​

Visit 7 at level 2
result.get(2).add(7); → result = [ [3], [9, 20], [15, 7] ]
Final result is [[3], [9, 20], [15, 7]], which is the level order traversal.
```

