## Problem Statement

You are given an `m x n` matrix M initialized with all 0's and an array of operations ops, where `ops[i] = [ai, bi]` means `M[x][y]` should be incremented by one for all `0 <= x < ai` and `0 <= y < bi`

Count and return the number of maximum integers in the matrix after performing all the operations.

<center> <img src="../images/range-additon-1.png" width="90%"> </center>

### Example 1

```bash
Input: m = 3, n = 3, ops = [[2,2],[3,3]]
Output: 4
Explanation: The maximum integer in M is 2, and there are four of it in M. So return 4.
```

### Example 2

```bash
Input: m = 3, n = 3, ops = [[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3]]
Output: 4
```

### Example 3

Here is another example

```bash
Input: m = 3, n = 3, ops = []
Output: 9

Constraints:

1 <= m, n <= 4 * 104
0 <= ops.length <= 104
ops[i].length == 2
1 <= ai <= m
1 <= bi <= n
```


## Solution
Upper left corner of the matrix can be represented by (0,0) and the lower right corner for an operation [i,j] is given by the index (i,j).

Also, the maximum element will be the one on which all the operations have been performed.

Let’s take an example:


<center> <img src="../images/range-additon-2.png" width="90%"> </center>


In the above figure, we can see that the maximum elements will be the ones that lie in the intersection region of the rectangles representing the operations.

Now, as the maximum number of operations will be done in the smallest such sub-matrix found so far, that is what we are interested in finding out

We can find this by taking the min for row and column bounds. The total number of elements will be then min_row_index * min_col_index


## Code

```bash
class Solution:
    def maxCount(self, m: int, n: int, ops: List[List[int]]) -> int:
        for r,c in ops:
            # expand and shrink the matrix size (bottom-right boundry of matrix) based on the current operation
            m = min(m,r)
            n = min(c,n)
        # total number of elements will be multiplication of bottom and right boundry asssming left and top boundry is 0,0
        return m*n
```