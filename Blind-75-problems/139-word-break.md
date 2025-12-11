### 139. Word Break

- Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

- Note that the same word in the dictionary may be reused multiple times in the segmentation.

 

Example 1:

Input: `s = "leetcode", wordDict = ["leet","code"]`
Output: `true`
Explanation: `Return true because "leetcode" can be segmented as "leet code".`
Example 2:

Input: `s = "applepenapple", wordDict = ["apple","pen"]`
Output: `true`
Explanation: `Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.`
Example 3:

Input: `s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]`
Output: `false`
 

Constraints:

1 <= s.length <= 300
1 <= wordDict.length <= 1000
1 <= wordDict[i].length <= 20
s and wordDict[i] consist of only lowercase English letters.
All the strings of wordDict are unique
## Solutions

### 1) DP Solution 
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordSet = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }

            }
        }
        return dp[s.length()];

    }
}
```

- Time complexity: O(n2)
- Space complexity: O(n)


#### Time Complexity
Outer loop: `i = 1 to n → n iterations`
Inner loop: `j = 0 to i → roughly n/2 average → n²/2 total`
substring(j,i): `O(n) time in worst case
→ Total: O(n³) naive, but **O(n²)** with optimizations `


#### Space Complexity
- dp array: O(n)
- wordSet: O(m * w) where m=wordDict.size(), w=avg word length
- Total: O(n + m*w) → **O(n)** dominant



####  Clean interview explanation
"Time O(n²): n positions × n possible cuts per position.
Space O(n): DP table + HashSet.
Optimal because we must verify all possible word breaks."


| Approach    | Time   | Space | Accepted? |
| ----------- | ------ | ----- | --------- |
|  DP     | O(n²)  | O(n)  | ✅ Optimal |
| Brute Force | O(2^n) | O(n)  | ❌ TLE     |
| Trie + DP   | O(n²)  | O(n)  | Same      |


### Hack to all DP
- #### Copy this FOREVER
```java
boolean[] dp = new boolean[n+1];
 dp[0]=true;
  for(int i=1;i<=n;i++)
    for(int j=0;j<i;j++) 
      if(dp[j] && isValid(s,j,i)) {
        dp[i]=true;break;
        }
  return dp[n];
  ```

- ####   For ANY DP problem:
```
1. "What does dp[i] mean?" → "Can reach position i?"
2. "How to reach i?"     → "Try ALL j < i where s[j:i] is word"
3. "Final answer?"       → "dp[n]"

Word Break = Q1:"reach i?", Q2:"word from j→i?", Q3:"dp[n]"
```



