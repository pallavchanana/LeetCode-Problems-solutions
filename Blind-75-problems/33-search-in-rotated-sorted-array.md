### 33. Search in Rotated Sorted Array
- Given an integer array nums sorted in ascending order (with distinct values), it is possibly rotated at an unknown pivot index.
- Given nums after rotation and an integer target, return the index of target if it is in nums, or -1 if it is not.

The array was originally sorted in strictly increasing order.

The array may or may not be rotated.

You must write an algorithm with O(log n) runtime complexity.

Examples
Example 1:

Input: nums = `[4,5,6,7,0,1,2]`, target = 0
Output: 4

Example 2:

Input: nums = `[4,5,6,7,0,1,2]`, target = 3
Output: -1

Example 3:

Input: nums = `[1]`, target = 0
Output: -1​

Constraints
1 <= nums.length <= 5000

-10^4 <= nums[i] <= 10^4

All values of nums are unique.

nums is an ascending array that is possibly rotated.

-10^4 <= target <= 10^4​

### Solutions
-  `Modified Binary Search (O(log n)) — Recommended`
At each step, one of the halves [start, mid] or [mid, end] is guaranteed to be sorted.
Use that to decide whether to discard the left half or right half while keeping O(log n) time.

```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            // Left half is sorted
            if (nums[start] <= nums[mid]) {
                if (nums[start] <= target && target < nums[mid]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            } else { // Right half is sorted
                if (nums[mid] < target && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

- Time complexity: O(log n)

- Space complexity: O(1)

```python
1) Python
Modified Binary Search (O(log n)) — Recommended
class Solution:
    def search(self, nums, target):
        start, end = 0, len(nums) - 1

        while start <= end:
            mid = start + (end - start) // 2

            if nums[mid] == target:
                return mid

            # Left half is sorted
            if nums[start] <= nums[mid]:
                if nums[start] <= target < nums[mid]:
                    end = mid - 1
                else:
                    start = mid + 1
            else:  # Right half is sorted
                if nums[mid] < target <= nums[end]:
                    start = mid + 1
                else:
                    end = mid - 1

        return -1
```
- Time complexity: O(log n)

- Space complexity: O(1)​

File: Blind-75-problems/33-search-in-rotated-sorted-array.md
Link - https://leetcode.com/problems/search-in-rotated-sorted-array/?envType=problem-list-v2&envId=oizxjoit

### Examples
Here are some “play in your head” examples to see how the logic works.​
```
Example 1: nums =, target = 0​​
start = 0 (4), end = 6 (2) → mid = 3 (7).
Left half is sorted because nums[start] ≤ nums[mid].​​
Check if target in left half: is 4 ≤ 0 < 7? No → discard left half, set start = mid + 1 = 4.
Now start = 4 (0), end = 6 (2) → mid = 5 (1).
Left half is sorted. Is 0 ≤ 0 < 1? Yes → move end = mid − 1 = 4.
start = 4, end = 4 → mid = 4 (0) == target → return 4.​


Example 2: nums =, target = 3​​
start = 0 (4), end = 6 (2) → mid = 3 (7). Left half sorted.​​
Is 4 ≤ 3 < 7? No → search right side, start = 4.
start = 4 (0), end = 6 (2) → mid = 5 (1). Left half sorted.​
Is 0 ≤ 3 < 1? No → search right side, start = 6.
start = 6 (2), end = 6 → mid = 6 (2). Left half is just.​
Is 2 ≤ 3 < 2? No → search right side, start = 7.
start > end → target not found → return −1.​
Example 3: nums =, target = 0​
start = 0, end = 0 → mid = 0 (1).
nums[mid] != target. Left half is and sorted.​
Is 1 ≤ 0 < 1? No → move start = mid + 1 = 1.
start > end → return −1.​
Example 4: nums =, target = 3​​
start = 0 (6), end = 7 (5) → mid = 3 (1).
Right half is sorted because nums[start] > nums[mid].​
Check if target in right half: is 1 ≤ 3 ≤ 5? Yes → move start = mid + 1 = 4.
start = 4 (2), end = 7 (5) → mid = 5 (3).
nums[mid] == target → return 5.​
```

Thinking like this when you code:
Decide which half is sorted.
Check if target lies in that sorted half.
Move start/end to keep only the relevant half.
