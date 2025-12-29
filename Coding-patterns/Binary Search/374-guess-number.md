### 374. Guess Number Higher or Lower - `Easy`
```
We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked (the number I picked stays the same throughout the game).

Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.

You call a pre-defined API int guess(int num), which returns three possible results:

-1: Your guess is higher than the number I picked (i.e. num > pick).
1: Your guess is lower than the number I picked (i.e. num < pick).
0: your guess is equal to the number I picked (i.e. num == pick).
Return the number that I picked.

 

Example 1:

Input: n = 10, pick = 6
Output: 6
Example 2:

Input: n = 1, pick = 1
Output: 1
Example 3:

Input: n = 2, pick = 1
Output: 1
 

Constraints:

1 <= n <= 231 - 1
1 <= pick <= n
```

### Intituion
```
The binary search intuition is like finding a specific page in a phone book by repeatedly guessing the middle and narrowing the range based on feedback.

Core Idea
Start with the full range [1, n]. Guess the exact middle number. The guess() API tells you if it's too high (-1), too low (1), or correct (0), cutting the search space in half each time. Repeat until you find it.
​
```

### Solution
```java
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int left = 1, right = n;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int guessNum = guess(mid);
            if (guessNum == 0) {
                return mid;
            } else if (guessNum == -1) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return -1;
    }
}
```

### Time and Space
- Time - `O(logn)`
- Space -`O(1)`