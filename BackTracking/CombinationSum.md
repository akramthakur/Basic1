# Combination Sum - Solution

## Problem Statement
Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. The same number may be chosen from `candidates` an unlimited number of times.

## Step-by-Step Logic

### Backtracking with Unlimited Choices:
1. **Include Current Element**: Add candidate to combination and recurse with same index (allows reuse)
2. **Exclude Current Element**: Skip current candidate and move to next index
3. **Base Case - Success**: When sum equals target, save current combination
4. **Base Case - Failure**: When sum exceeds target or no more candidates

## Complexity Analysis

### Time Complexity: **O(2^target)**
- **Exponential** in worst case as each candidate can be chosen multiple times
- **Branching factor** depends on target value and candidate values
- More precisely: **O(N^(target/min_candidate + 1))**

### Space Complexity: **O(target/min_candidate)**
- **O(target/min_candidate)** for recursion call stack depth
- **O(target/min_candidate)** for current combination storage
- **Output space** depends on number of valid combinations

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(vector<vector<int>>& ans, vector<int>& nums, int i, int sum, vector<int>& candidates) {
        // Base case: found valid combination that sums to target
        if(sum == 0) {
            ans.push_back(nums);
            return;
        }
        
        // Base case: sum exceeded or no more candidates
        if(sum < 0 || i >= candidates.size()) {
            return;
        }
        
        // Include current candidate (can be reused)
        nums.push_back(candidates[i]);
        rec(ans, nums, i, sum - candidates[i], candidates);  // Same index for reuse
        nums.pop_back();  // Backtrack
        
        // Exclude current candidate and move to next
        rec(ans, nums, i + 1, sum, candidates);
    }
    
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;  // Store all valid combinations
        vector<int> num;          // Current combination being built
        rec(ans, num, 0, target, candidates);
        return ans;
    }
};
