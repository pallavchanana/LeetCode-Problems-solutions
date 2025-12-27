### 5. Longest Palindromic Substring -`  Medium`

Hint
Given a string s, return the longest palindromic substring in s.

 

Example 1:

Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
Example 2:

Input: s = "cbbd"
Output: "bb"

## Solution
```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() < 1) {
            return "";
        }

        int start = 0;
        int end = 0;

        for (int i = 0; i < s.length(); i++) {
            int len1 = expandAroundCenter(s, i, i);     // odd-length center
            int len2 = expandAroundCenter(s, i, i + 1); // even-length center
            int len = Math.max(len1, len2);

            if (len > end - start) {
                // compute updated start and end based on current center i
                start = i - (len - 1) / 2;
                end   = i + len / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    private int expandAroundCenter(String s, int left, int right) {
        // Expand as long as we are in bounds and characters match
        while (left >= 0 && right < s.length()
               && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        // When loop ends, indices have gone one step too far
        return right - left - 1;
    }
}

```

How optimal is this approach?
### Time complexity:

There are 
`O(n)` possible centers.

Each expansion can scan up to 
`O(n)` characters in the worst case.

Overall 
`O(n2)` time.
​

### Space complexity:
Only a few variables for indices and lengths.

Overall 
`O(1)` extra space.