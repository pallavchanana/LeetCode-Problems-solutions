# 1.Two Sum

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

- You may assume that each input has exactly one solution.
- You may not use the same element twice.
- You can return the answer in any order.

## Examples

Example 1:

Input: `nums = [2,7,11,15]`, `target = 9`  
Output: `[0,1]`  
Explanation: `nums[0] + nums[1] == 9`.

Example 2:

Input: `nums = [3,2,4]`, `target = 6`  
Output: `[1,2]`

Example 3:

Input: `nums = [3,3]`, `target = 6`  
Output: `[0,1]`

## Constraints

- `2 <= nums.length <= 10^4`  
- `-10^9 <= nums[i] <= 10^9`  
- `-10^9 <= target <= 10^9`  
- Exactly one valid answer exists.

## Follow-up
Can you come up with an algorithm that is better than O(n^2) time complexity?

---

## Solutions

### 1) Brute-force (O(n^2))
Simple double loop. Fixed the inner loop to start from `i+1` to avoid checking the same pair twice.

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[] { i, j };
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```

- Time complexity: O(n^2)
- Space complexity: O(1)

### 2) One-pass HashMap (O(n)) — Recommended
Use a HashMap to store value → index while iterating. For each element, check if its complement (target - nums[i]) already exists in the map.

```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> numsMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (numsMap.containsKey(complement)) {
                return new int[] { numsMap.get(complement), i };
            }
            numsMap.put(nums[i], i);
        }
        throw new IllegalArgumentException("Not found");
    }
}
```

- Time complexity: O(n)
- Space complexity: O(n)

---

### 1) Python 
One-pass Dictionary (O(n)) — Recommended

Use a dictionary to store value → index while iterating. For each element, check if its complement (target - nums[i]) already exists in the dictionary.

```python
class Solution:
    def twoSum(self, nums, target):
        nums_map = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in nums_map:
                return [nums_map[complement], i]
            nums_map[num] = i
        raise ValueError("No two sum solution")
```

- Time complexity: O(n)
- Space complexity: O(n)

File: `Blind-75-problems/1-two-sum.md`
Link- https://leetcode.com/problems/two-sum/?envType=problem-list-v2&envId=oizxjoit