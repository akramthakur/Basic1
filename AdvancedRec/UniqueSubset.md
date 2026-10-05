# Unique Subsets - Solution

## Problem Statement
Given an array `arr` of integers that may contain duplicates, return all possible unique subsets. The solution must not contain duplicate subsets.

## Step-by-Step Logic

### Backtracking with Duplicate Handling:
1. **Sort Array**: Sort input to group duplicates together
2. **Include Branch**: Add current element to subset and recurse
3. **Skip Duplicates**: After excluding, skip all consecutive duplicates
4. **Exclude Branch**: Skip current element and move to next unique element
5. **Base Case**: When all elements are processed, save current subset

## Complexity Analysis

### Time Complexity: **O(2^n)**
- **O(2^n)** total subsets in worst case (all unique elements)
- **O(n log n)** for sorting the array
- **n** = number of elements in input array

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
        
        // Skip all consecutive duplicates to avoid duplicate subsets
        while(i + 1 < nums.size() && nums[i] == nums[i + 1])
            i++;
            
        rec(ans, nums, i + 1, j);  // Recurse with element excluded and duplicates skipped
    }
    
    vector<vector<int>> findSubsets(vector<int>& arr) {
        vector<vector<int>> ans;  // Store all unique subsets
        vector<int> j;           // Current subset being built
        
        sort(arr.begin(), arr.end());  // Sort to group duplicates
        rec(ans, arr, 0, j);          // Start recursion from index 0
        
        return ans;
    }
};
