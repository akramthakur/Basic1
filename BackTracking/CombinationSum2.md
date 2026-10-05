# Combination Sum II - Solution

## Problem Statement
Given a collection of candidate numbers `candidates` (which may contain duplicates) and a target number `target`, find all unique combinations in `candidates` where the candidate numbers sum to `target`. Each number in `candidates` may only be used once in the combination.

## Step-by-Step Logic

### Backtracking with Duplicate Handling:
1. **Sort Array**: Sort candidates to group duplicates together
2. **Iterate through candidates**: For each position, try including current candidate
3. **Skip Duplicates**: Skip consecutive duplicates to avoid duplicate combinations
4. **Prune Search**: Stop if current candidate exceeds remaining sum
5. **Base Case - Success**: When sum equals target, save current combination
6. **Base Case - Failure**: When sum exceeds target or no more candidates

## Complexity Analysis

### Time Complexity: **O(2^n)**
- **O(2^n)** in worst case (all unique elements)
- **O(n log n)** for sorting the candidates
- **n** = number of candidates

### Space Complexity: **O(n)**
- **O(n)** for recursion call stack depth
- **O(n)** for current combination storage
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
        
        // Try each candidate starting from current index
        for(int j = i; j < candidates.size(); j++) {
            // Skip duplicates to avoid duplicate combinations
            if(j > i && candidates[j] == candidates[j - 1])
                continue;
            
            // Prune: if candidate exceeds remaining sum, no need to check further
            if(candidates[j] > sum)
                break;
            
            // Include current candidate
            nums.push_back(candidates[j]);
            
            // Recurse with next index (j+1) since each candidate can be used only once
            rec(ans, nums, j + 1, sum - candidates[j], candidates);
            
            // Backtrack
            nums.pop_back();
        }
    }
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> ans;  // Store all valid combinations
        vector<int> num;          // Current combination being built
        
        // Sort to handle duplicates efficiently
        sort(candidates.begin(), candidates.end());
        rec(ans, num, 0, target, candidates);
        
        return ans;
    }
};
