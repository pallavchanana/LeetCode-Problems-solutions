# 79. Word Search
### Level - `Medium`
Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid. [web:14][web:28]

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once. [web:14][web:28]

Problem link: https://leetcode.com/problems/word-search/

---

## Examples

**Example 1**

Input:  
`board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "ABCCED"`  
Output: `true`

**Example 2**

Input:  
`board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "SEE"`  
Output: `true`

**Example 3**

Input:  
`board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, `word = "ABCB"`  
Output: `false` [web:14][web:28]

---

## Constraints

- `m == board.length`  
- `n == board[i].length`  
- `1 <= m, n <= 6`  
- `1 <= word.length <= 15`  
- `board` and `word` consist of only uppercase and lowercase English letters. [web:13][web:27]

---

## Approach

Use DFS with backtracking starting from every cell that can match the first character of `word`. 

At each step:

- Check bounds and whether `board[i][j]` matches `word[count]`.  
- Temporarily mark the cell as visited by overwriting it (e.g., with `' '`), so it is not reused in the same path.  
- Recurse into four directions (up, down, left, right) for the next character.  
- Restore the original character on backtrack.  

This stops early as soon as a complete match for the whole word is found.

---

## Java: DFS + Backtracking (O(m · n · 4^L))
```
class Solution {
    public boolean exist(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                
                // Start DFS when first character matches
                if (board[i][j] == word.charAt(0) && helper(board, word, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean helper(char[][] board, String word, int i, int j, int count) {
        // All characters matched
        if (count == word.length()) {
            return true;
        }

        // Out of bounds or mismatch
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(count)) {
            return false;
        }

        // Mark current cell as visited
        char temp = board[i][j];
        board[i][j] = ' ';

        // Explore in 4 directions
        boolean found = helper(board, word, i + 1, j, count + 1) ||
                helper(board, word, i - 1, j, count + 1) ||
                helper(board, word, i, j + 1, count + 1) ||
                helper(board, word, i, j - 1, count + 1);
        board[i][j] = temp;
        return found;
    }
}
```


- Time complexity: \(O(m \cdot n \cdot 4^L)\), where \(m, n\) are board dimensions and \(L\) is `word.length`. 
- Space complexity: \(O(L)\) recursion depth (in-place marking avoids extra visited matrix).
