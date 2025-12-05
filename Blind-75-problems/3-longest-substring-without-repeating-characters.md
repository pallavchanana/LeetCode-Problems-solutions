# 3. Longest Substring Without Repeating Characters
Difficulty — Medium

Given a string `s`, find the length of the longest substring without duplicate characters.

## Examples

Example 1:

Input: `s = "abcabcbb"`  
Output: `3`  
Explanation: The answer is "abc", with length `3`. ("bca" and "cab" also valid substrings.)

Example 2:

Input: `s = "bbbbb"`  
Output: `1`  
Explanation: The answer is "b".

Example 3:

Input: `s = "pwwkew"`  
Output: `3`  
Explanation: The answer is "wke". Note that "pwke" is a subsequence, not a substring.

## Constraints

- `0 <= s.length <= 5 * 10^4`
- `s` consists of English letters, digits, symbols and spaces.

---

## Solutions

###     1) Sliding Window (O(n)) — Recommended
Use a sliding window with a map (or array for limited charset) to remember the last seen index of each character. Move the window start to avoid duplicates while scanning once.

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
	public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
		Map<Character, Integer> charIndexMap = new HashMap<>();
		int maxLength = 0;
		int start = 0;

		for (int end = 0; end < s.length(); end++) {
			char currentChar = s.charAt(end);
			if (charIndexMap.containsKey(currentChar)) {
				start = Math.max(start, charIndexMap.get(currentChar) + 1);
			}
			charIndexMap.put(currentChar, end);
			maxLength = Math.max(maxLength, end - start + 1);
		}

		return maxLength;
	}
}
```

- Time complexity: O(n)
- Space complexity: O(min(n, m)) where `m` is the size of the charset (map stores seen characters).

### 3) Sliding-window (ASCII-optimized using `int[]`)
If the input is known to be ASCII (or a small fixed charset), an `int[]` indexed by the character code is faster than a HashMap.

```java
import java.util.Arrays;

public class Solution {
	public int lengthOfLongestSubstring(String s) {
		if (s == null || s.length() == 0) return 0;
		// use 128 for standard ASCII, 256 for extended ASCII
		int[] last = new int[128];
		Arrays.fill(last, -1);
		int max = 0;
		int start = 0;

		for (int i = 0; i < s.length(); i++) {
			char c = s.charAt(i);
			if (last[c] >= start) {
				start = last[c] + 1;
			}
			last[c] = i;
			max = Math.max(max, i - start + 1);
		}
		return max;
	}
}
```

- Time complexity: O(n)
- Space complexity: O(1) (fixed-size `int[]`)

### Python (one-pass sliding window)


```python
class Solution:
	def lengthOfLongestSubstring(self, s: str) -> int:
		last = {}
		start = 0
		maxlen = 0
		for i, ch in enumerate(s):
			if ch in last and last[ch] >= start:
				start = last[ch] + 1
			last[ch] = i
			maxlen = max(maxlen, i - start + 1)
		return maxlen
```




File: `Blind-75-problems/3-longest-substring-without-repeating-characters.md`
URL- https://leetcode.com/problems/longest-substring-without-repeating-characters/submissions/1290135190/?envType=problem-list-v2&envId=oizxjoit