# Permutations - Solution

## Problem Statement
Given an array `nums` of distinct integers, return all possible permutations. You can return the answer in any order.

## Step-by-Step Logic

### Backtracking/Swapping Approach:
1. **Fix Position**: Start from index `i` and try all elements from `i` to end
2. **Swap Elements**: Place each possible element at position `i` by swapping
3. **Recurse**: Generate permutations for remaining positions (i+1 to end)
4. **Backtrack**: Restore original order by swapping back
5. **Base Case**: When all positions are fixed, save current permutation

## Complexity Analysis

### Time Complexity: **O(n × n!)**
- **O(n!)** total permutations generated
- **O(n)** time per permutation for swapping and copying
- **n** = number of elements in input array

### Space Complexity: **O(n)**
- **O(n)** for recursion call stack depth
- **O(n!)** for output storage (not counted in auxiliary space)
- **O(1)** extra space for swapping operations

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(vector<vector<int>>& ans, vector<int>& nums, int i) {
        // Base case: all positions fixed, save current permutation
        if(i == nums.size()) {
            ans.push_back(nums);
            return;
        }

        // Try all possible elements at position i
        for(int k = i; k < nums.size(); k++) {
            // Place nums[k] at position i
            swap(nums[k], nums[i]);
            
            // Recursively generate permutations for remaining positions
            rec(ans, nums, i + 1);
            
            // Backtrack: restore original order
            swap(nums[k], nums[i]);
        }
    }
    
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;  // Store all permutations
        rec(ans, nums, 0);       // Start generating from index 0
        return ans;
    }
};
