# Subsets - Solution

## Problem Statement
Given an integer array `nums` of unique elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets.

## Step-by-Step Logic

### Backtracking/Recursive Approach:
1. **For each element**: Make a choice to either include or exclude it
2. **Include Branch**: Add current element to subset and recurse
3. **Exclude Branch**: Skip current element and recurse
4. **Base Case**: When all elements are processed, save current subset
5. **Backtrack**: Remove last element to explore other possibilities

## Complexity Analysis

### Time Complexity: **O(2^n)**
- **O(2^n)** total subsets generated
- **n** = number of elements in input array
- Each element has 2 choices: include or exclude

### Space Complexity: **O(n)**
- **O(n)** for recursion call stack depth
- **O(n)** for current subset storage
- **O(2^n)** for output storage (not counted in auxiliary space)

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(vector<vector<int>>& ans, vector<int>& nums, int i, vector<int>& j) {  
        // Base case: processed all elements, save current subset
        if(i == nums.size()) {
            ans.push_back(j);
            return;
        }
        
        // Include current element
        j.push_back(nums[i]);
        rec(ans, nums, i + 1, j);  // Recurse with element included
        
        // Exclude current element (backtrack)
        j.pop_back();
        rec(ans, nums, i + 1, j);  // Recurse with element excluded
    }
    
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;  // Store all subsets
        vector<int> j;           // Current subset being built
        rec(ans, nums, 0, j);    // Start recursion from index 0
        return ans;
    }
};
