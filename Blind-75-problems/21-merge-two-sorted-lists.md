# 21. Merge Two Sorted Lists

Difficulty — Easy

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

## Examples

Example 1:

Input: `list1 = [1,2,4]`, `list2 = [1,3,4]`  
Output: `[1,1,2,3,4,4]`  
Explanation: Merge by always taking the smaller node.

Example 2:

Input: `list1 = []`, `list2 = []`  
Output: `[]`

Example 3:

Input: `list1 = []`, `list2 = [0]`  
Output: `[0]`

## Constraints

- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `list1` and `list2` are sorted in non-decreasing order.

---

## Solutions

### 1) Brute force Solution: ArrayList + Sort (O(n log n) time)
Extract all values into an ArrayList, sort it, then rebuild the linked list from scratch.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // Step 1: Extract all values from both lists into an ArrayList
        ArrayList<Integer> newList = new ArrayList<Integer>();
        while (list1 != null) {
            newList.add(list1.val);
            list1 = list1.next;
        }
        while (list2 != null) {
            newList.add(list2.val);
            list2 = list2.next;
        }
        
        // Step 2: Sort the combined list
        Collections.sort(newList);
        
        // Step 3: Rebuild a linked list from sorted values
        // Dummy node helps: always has a 'next' pointer to attach to
        ListNode dummy = new ListNode(-1);
        ListNode curr = dummy;
        
        for (int i = 0; i < newList.size(); i++) {
            curr.next = new ListNode(newList.get(i));
            curr = curr.next;
        }
        return dummy.next; // return the first real node (skip dummy)
    }
}
```

- Time complexity: O(n log n) — dominated by sorting
- Space complexity: O(n) — ArrayList stores all values

### 2) Two-Pointer Merge (O(n) time) — Recommended
Since both lists are already sorted, compare nodes from each list and attach the smaller one. This is the **optimal** approach: no sorting needed, no extra list allocation.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // Create a dummy node to simplify logic (no special handling for first node)
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy; // pointer to build the merged list
        
        // Compare nodes from both lists and attach the smaller one
        // Continue while both lists have remaining nodes
        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                // list1's node is smaller or equal, attach it
                curr.next = list1;
                list1 = list1.next; // move to next node in list1
            } else {
                // list2's node is smaller, attach it
                curr.next = list2;
                list2 = list2.next; // move to next node in list2
            }
            curr = curr.next; // move curr forward in the merged list
        }
        
        // After loop, one list is empty, one may have remaining nodes
        // Attach the entire remaining part of whichever list has nodes left
        if (list1 != null) {
            curr.next = list1;
        } else {
            curr.next = list2;
        }
        
        // Return first real node (skip dummy which has value 0)
        return dummy.next;
    }
}
```

- Time complexity: O(n + m) where n, m are lengths of list1, list2
- Space complexity: O(1) — only uses pointers, no extra data structures

### Step-by-step walkthrough: list1 = [1,2,4], list2 = [1,3,4]

Initial: dummy → null, curr → dummy, list1 → 1, list2 → 1

**Iteration 1:** list1.val(1) <= list2.val(1)  
- Attach list1's node: curr.next = list1  
- Move list1 to next: list1 = 2  
- Move curr forward: curr → 1  

**Iteration 2:** list1.val(2) > list2.val(1)  
- Attach list2's node: curr.next = list2  
- Move list2 to next: list2 = 3  
- Move curr forward: curr → 1(from list2)  

**Iteration 3:** list1.val(2) <= list2.val(3)  
- Attach list1's node: curr.next = list1  
- Move list1 to next: list1 = 4  
- Move curr forward: curr → 2  

**Iteration 4:** list1.val(4) > list2.val(3)  
- Attach list2's node: curr.next = list2  
- Move list2 to next: list2 = 4  
- Move curr forward: curr → 3  

**Iteration 5:** list1.val(4) <= list2.val(4)  
- Attach list1's node: curr.next = list1  
- Move list1 to next: list1 = null  
- Move curr forward: curr → 4(from list1)  

**Loop ends** (list1 is null)  
- Attach remaining list2: curr.next = list2 (which points to 4)  

**Result:** dummy.next = [1,1,2,3,4,4] ✓



File: `Blind-75-problems/21-merge-two-sorted-lists.md`