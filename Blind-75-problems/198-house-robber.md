## 198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

 

#### Example 1:

Input: nums =`[1,2,3,1]`
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: nums = `[2,7,9,3,1]`
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.

# Solution
```java
class Solution {
    public int rob(int[] nums) {
        //exit condtions
        if (nums.length == 0)
            return 0;
        if (nums.length == 1)
            return nums[0];
        // initialise    
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i < nums.length; i++) {
            int skipthishouse = dp[i - 1];
            int robthishouse = dp[i - 2] + nums[i];
            dp[i] = Math.max(skipthishouse, robthishouse);
        }
        return dp[nums.length - 1];
    }
}
```

### Example 1: `[1,2,3,1] → 4`
```
House:  0  1  2  3
Value:  1  2  3  1
dp:     1  2  3  4

i=2: max(dp[1]=2, dp[0]+3=4) → dp[2]=4  (rob 0+2:1+3)
i=3: max(dp[2]=4, dp[1]+1=3) → dp[3]=4  (skip 3)

Rob houses 0 and 2: 1+3=4 (cannot rob 1+2=3, adjacent!)
```

### Example 2: `[2,7,9,3,1] → 12`
```
House:  0  1  2  3  4
Value:  2  7  9  3  1
dp:     2  7 11 11 12

i=2: max(7, 2+9=11) → 11
i=3: max(11, 7+3=10) → 11  
i=4: max(11, 11+1=12) → 12


Rob 0,2,4: 2+9+1=12
```

### Example 3: `[1,3,1,3,100] → 103`
```
House:  0  1  2  3  4
Value:  1  3  1  3 100
dp:     1  3  4  6 103

i=4: max(dp[3]=6, dp[2]+100=104) → 104? Wait!
Wait: dp[2]=4, 4+100=104 ✓

Rob 1 and 4: 3+100=103 (or 0+2+4=102)


```


