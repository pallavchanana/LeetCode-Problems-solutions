### 34. Find First and Last Position of Element in Sorted Array -` Medium`
Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
Example 2:

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
Example 3:

Input: nums = [], target = 0
Output: [-1,-1]
 

Constraints:

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums is a non-decreasing array.
-109 <= target <= 109

### Intituion
```
Use binary search twice to find the first and last index of target in the sorted array.
​
First search (firstPos):
Standard binary search on [left, right].
When nums[mid] == target, store mid as firstIndex, then move right = mid - 1 to keep looking on the left side.

Second search (LastPos):
Same idea, but when nums[mid] == target, store mid as lastIndex, then move left = mid + 1 to keep looking on the right side.
Return [firstIndex, lastIndex] or [-1, -1] if not found
```
 ### Solution
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return new int[] { -1, -1 };
        }
        int first = firstPos(nums, target);
        if (first == -1) {
            return new int[] { -1, -1 };
        }
        int last = LastPos(nums, target);
        return new int[] { first, last };
    }

    private int firstPos(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int firstIndex = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                firstIndex = mid;
                right = mid - 1;
            }
            else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return firstIndex;
    }

    private int LastPos(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int lastIndex = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                lastIndex = mid;
                left = mid + 1;
            }
            else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return lastIndex;
    }
}
```

### Time and Space
- Time - `O(logn)`
- Space -`O(1)`