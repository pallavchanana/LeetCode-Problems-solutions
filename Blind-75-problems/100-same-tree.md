
 

# 100. Same Tree

Difficulty — Easy

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

## Examples

Example 1:

Input: `p = [1,2,3]`, `q = [1,2,3]`  
Output: `true`

Example 2:

Input: `p = [1,2]`, `q = [1,null,2]`  
Output: `false`

Example 3:

Input: `p = [1,2,1]`, `q = [1,1,2]`  
Output: `false`

## Constraints

- The number of nodes in both trees is in the range `[0, 100]`.
- `-10^4 <= Node.val <= 10^4`

---

## Solutions

### 1) Your recursive solution (simple DFS)
I added your exact implementation below — it's a correct recursive depth-first solution. I only wrapped it in the standard TreeNode comment header for context.

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
	public boolean isSameTree(TreeNode p, TreeNode q) {
		if(p == null && q == null){
			return true;
		}
		if(p != null && q != null && p.val == q.val){
			return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
		}
		return false;
	}
}
```

- Time complexity: O(n) — each node is visited once
- Space complexity: O(h) recursion stack where h is tree height

### 2) Iterative (BFS) — alternative for interviews
If you want an iterative version to present in interviews, here is a queue-based approach that compares node pairs.

```java
import java.util.ArrayDeque;
import java.util.Deque;

class Solution {
	public boolean isSameTree(TreeNode p, TreeNode q) {
		Deque<TreeNode[]> dq = new ArrayDeque<>();
		dq.add(new TreeNode[] {p, q});

		while (!dq.isEmpty()) {
			TreeNode[] pair = dq.removeFirst();
			TreeNode a = pair[0], b = pair[1];
			if (a == null && b == null) continue; // both null -> OK
			if (a == null || b == null) return false; // structure mismatch
			if (a.val != b.val) return false; // value mismatch
			dq.addLast(new TreeNode[] {a.left, b.left});
			dq.addLast(new TreeNode[] {a.right, b.right});
		}
		return true;
	}
}
```

- Time complexity: O(n)
- Space complexity: O(n) in worst case for the queue

---

## Interview tips

- Explain the recursive approach first: check nulls, check values, recurse on left and right.
- Mention edge cases: both null → true, one null → false.
- Complexity: O(n) time, O(h) space (recursion or queue).

File: `Blind-75-problems/100-same-tree.md`