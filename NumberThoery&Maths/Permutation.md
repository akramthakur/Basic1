# Permutations - Solution

## Problem Statement
Given an array of distinct integers, return all possible permutations.

## Step-by-Step Logic

### Algorithm:
1. **Backtracking Approach**: Generate all permutations by swapping elements
2. **Recursive Generation**: At each position, try all possible elements that haven't been used
3. **Swap-based**: Avoid extra space by swapping elements in place

### Key Insight:
- Fix one element at current position, recursively generate permutations for remaining elements
- Use swapping to try different elements at each position
- Backtrack by swapping back to restore original state

## Complexity Analysis

### Time Complexity: **O(n × n!)**
- n! permutations
- O(n) time to copy each permutation to result

### Space Complexity: **O(n)**
- Recursion stack depth: O(n)
- Output space: O(n × n!) not counted as extra space

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(vector<vector<int>>& ans, vector<int>& nums, int i) {
        // Base case: reached end of array
        if (i == nums.size()) {
            ans.push_back(nums);  // Add current permutation to result
            return;
        }

        // Generate permutations by swapping elements
        for (int k = i; k < nums.size(); k++) {
            // Swap to put nums[k] at position i
            swap(nums[k], nums[i]);
            
            // Recursively generate permutations for remaining positions
            rec(ans, nums, i + 1);
            
            // Backtrack: restore original order
            swap(nums[k], nums[i]);
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        rec(ans, nums, 0);
        return ans;
    }
};
