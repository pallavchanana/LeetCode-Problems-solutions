# 268. Missing Number

Difficulty — Easy

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

## Examples

Example 1:

Input: `nums = [3,0,1]`  
Output: `2`  
Explanation: `n = 3` since there are 3 numbers, so all numbers are in the range `[0,3]`. `2` is the missing number.

Example 2:

Input: `nums = [0,1]`  
Output: `2`  
Explanation: `n = 2`; `2` is missing.

Example 3:

Input: `nums = [9,6,4,2,3,5,7,0,1]`  
Output: `8`  
Explanation: `n = 9`; `8` is missing.

## Constraints

- `n == nums.length`
- `1 <= n <= 10^4`
- `0 <= nums[i] <= n`
- All the numbers of `nums` are unique.

---

## Solutions

### 1) Gauss sum formula (O(n) time, O(1) space)
Compute the expected sum of numbers `0..n` using `n*(n+1)/2`, subtract the actual sum of `nums` to get the missing number. Use a `long` accumulator to avoid overflow in languages with limited integer sizes.

```java
1) Java variant (sum using loop)
This version computes the sum of array elements and the sum of `1..n` via a loop, then returns their difference. It is equivalent to the Gauss formula approach but uses explicit accumulation.

public class Solution {
    public int missingNumber(int[] nums) {
        int total = 0; // sum of array elements
        int sum = 0;   // sum of 1..n
        for (int i = 0; i < nums.length; i++) {
            total += nums[i];
            sum += i + 1; // accumulate 1..n
        }
        return sum - total;
    }
}
```


- Time complexity: O(n)
- Space complexity: O(1)

### 2) XOR (O(n) time, O(1) space) — Recommended
Use XOR to cancel out pairs: XOR all indices `0..n` with all array values; the remaining value is the missing number.

```java
public class Solution {
    public int missingNumber(int[] nums) {
        int xor = 0;
        int n = nums.length;
        // XOR all indices 0..n
        for (int i = 0; i <= n; i++) {
            xor ^= i;
        }
        // XOR all array values
        for (int x : nums) xor ^= x;
        return xor; // leftover is the missing number
    }
}
```

- Time complexity: O(n)
- Space complexity: O(1)

### 3) Sorting (O(n log n) time)
Sort `nums` and scan for the first index `i` where `nums[i] != i`. Not recommended for optimal runtime, but simple.

```java
import java.util.Arrays;

public class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != i) return i;
        }
        return nums.length; // all matched, missing is n
    }
}
```



File: `Blind-75-problems/268-missing-muber.md`
URl - https://leetcode.com/problems/missing-number/?envType=problem-list-v2&envId=oizxjoit