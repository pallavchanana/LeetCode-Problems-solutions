### 39. Combination Sum - `Medium`
- Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

- The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

- The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

 
```
Example 1:

Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
Example 2:

Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
Example 3:

Input: candidates = [2], target = 1
Output: []
 

Constraints:

1 <= candidates.length <= 30
2 <= candidates[i] <= 40
All elements of candidates are distinct.
1 <= target <= 40
```

## Solution
- Use backtracking with a “take or skip” choice at each index, building a current combination list while reducing the remaining target, and whenever the target hits zero, add a copy of the current list to the result.

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> current = new ArrayList<>();
        if (candidates.length == 0) {
            return result;
        }
        backtrack(candidates, target, 0, current, result);
        return result;

    }

    private void backtrack(int[] candidates, int target, int index, List<Integer> current, List<List<Integer>> result) {
        if (target == 0) {
            //new ArrayList<>(current) creates a copy of the current path.
            //That copy is put into result.
            result.add(new ArrayList<>(current));
            return;
        }
        if (target < 0 || index == candidates.length) {
            //out of bound
            return;
        }
        current.add(candidates[index]);
        backtrack(candidates, target - candidates[index], index, current, result);
        current.remove(current.size() - 1);
        backtrack(candidates, target, index + 1, current, result);
    }
}
```

### Time Complexiety
`O(2n)`
- Time complexity is exponential in the worst case because we explore all subsets/combinations that can sum up to target.”


### Space Complexiety
- Auxiliary space is O(T) due to recursion and the current path, but total space including results is exponential in the worst case.


## Notes
```
Understand each line’s role
Using:

java
current.add(candidates[index]);
backtrack(candidates, target - candidates[index], index, current, result);
current.remove(current.size() - 1);
backtrack(candidates, target, index+1, current, result);
Map it to meaning:

current.add(candidates[index]);
→ “Try taking this number; put it into the current combination.”

backtrack(... target - candidates[index], index, ...)
→ “Stay at same index (can reuse same number), and reduce remaining target.”

current.remove(current.size() - 1);
→ “Undo that choice (backtrack) so current goes back to the previous state.”

backtrack(... target, index+1, ...)
→ “Try the other choice: skip this number and move to the next index.”

If you remember just:
“take → recurse → undo → skip”, you can always rebuild the code.

Simple mnemonic
For backtracking with choices:

1 Take it

2 Recurse

3 Undo it

4 Skip it

```