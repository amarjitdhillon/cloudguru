---
icon: material/image-size-select-small
---

# Combination Sum

<figure markdown>
  ![combinationSum](/images/combinationSum01.jpeg){ loading=lazy }
</figure>


## [Problem Statement- Leetcode 39](https://leetcode.com/problems/combination-sum/)  

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order. 
The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.
It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

### Examples

```properties
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

```

### Constraints
```properties
 
    1 <= candidates.length <= 30
    
    1 <= candidates[i] <= 200
    
    All elements of candidates are distinct.
    
    1 <= target <= 500
```

## Intution

- We can use the backtracking approach here, in which once we determime that we are not able proceed further down in the tree node, we can backtrack to parent node and explore other possibilities



## Algorithm
1. We can leverage a backtracking solution using DFS. Here, we can create a `DFS` function and call it recursively from the main function.

1. Initialize an empty result list to hold the output which will be returned at the end.

1.  Define a recursive function named `#!python dfs(remain, arr, idx)` which explores various combinations, starting from the current combination (stored in arr), the remaining sum (remain) and the current position in candidate array ( represented by idx). 
    
    1. In recursion, the base case is the case in which we define when to backtrack. Here we will have 2 base cases:
      
    1. $1^{st}$ base case: `#!python if remain==0`, i.e. we fulfill the desired target sum, therefore we can add the current combination to the final list (named result).
    
    1. $2^{nd}$ base case: `if remain < 0`, i.e. we exceed the target value, we will cease the exploration here and return.
    
    1. Otherwise, we will explore the various other possibilities starting from the current cursor position, represented by ` idx`. For each of the candidate, we invoke the recursive function itself with updated parameters. These paramenters are:
    
        1. `remain`: We will reduce this to `remain - current candidate node` as the pending remaining value will reduce for next the exporation.
        1. `arr`: We need to update the `arr` list by adding the `current candidate node's value` to the `arr`. 
        1. `idx`: Set this to the current index as the next exporation can start from the `current idx` onwards (including the current index value) 
     
    1. At the end of each exploration, we backtrack by popping out the candidate node out of the combination list (represented by `arr`) using the pop() function. In `Python`, using `pop(-1) or pop(0)` will do this job.
    
    1. Return the result list at end of the DFS.

1. In the driver program, call the DFS function with `remain` as `target`, `arr` as `[]` and `idx` as 0

## Solution

```py title="Combination Sum"
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        result = []
        
        # here remain is the remainingSum, arr is the array formed so far, idx is the id of the current num in candidates
        def dfs(remain, arr, idx):
            # base case: add the arr to the result array. Make a deep copy
            if remain == 0:
                result.append(list(arr))
                return 
            
            # base case: if the remain is < 0, then we need to backtrack
            if remain < 0:
                return
            
            # else explore all the possible cases
            for i in range(idx, len(candidates)):
                arr.append(candidates[i])
                
                # explore all the possible cases from the current idx onwards
                dfs(remain - candidates[i], arr, i)
                
                # remove the last element
                arr.pop(-1)
                
            return result

        # driver code
        return dfs(target, [], 0)
```
