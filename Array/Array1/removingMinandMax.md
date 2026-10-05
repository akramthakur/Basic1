# Minimum Deletions to Remove Minimum and Maximum - Solution

## Problem Statement
Given an array, find the minimum number of deletions required to remove both the minimum and maximum elements from the array. Deletions can be done from the front, back, or both ends.

## Step-by-Step Logic

1. **Find Extreme Elements**:
   - Locate indices of minimum and maximum elements
   - Track both positions during single array traversal

2. **Calculate Three Deletion Strategies**:
   - **Delete from front only**: Remove all elements up to the farther extreme
   - **Delete from back only**: Remove all elements after the nearer extreme  
   - **Delete from both ends**: Remove from front up to nearer extreme + from back after farther extreme

3. **Return Minimum**:
   - Compare all three strategies and return the smallest deletion count

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through array to find min/max indices: O(n)
- Constant time operations for deletion calculations

### Space Complexity: **O(1)**
- Only using fixed variables for indices and values
- No additional data structures

## Final Code with Comments

```cpp
class Solution {
public:
    int minimumDeletions(vector<int>& nums) {
        // Initialize variables to track extremes
        int maxi = INT_MIN;
        int mini = INT_MAX;
        int indmax = 0;
        int indmin = 0;
        
        // Find indices of minimum and maximum elements
        for(int i = 0; i < nums.size(); i++){
            if(nums[i] > maxi){
                maxi = nums[i];
                indmax = i;
            }
            if(nums[i] < mini){
                mini = nums[i];
                indmin = i;
            }
        }
        
        int n = nums.size();
        
        // Strategy 1: Delete all from front (up to farther extreme)
        int deletefront = max(indmax, indmin) + 1;
        
        // Strategy 2: Delete all from back (after nearer extreme)  
        int deleteback = n - min(indmax, indmin);
        
        // Strategy 3: Delete from both ends
        int delfromboth = (min(indmax, indmin) + 1) + (n - (max(indmax, indmin)));
        
        // Return the minimum of all three strategies
        return min(delfromboth, min(deletefront, deleteback));
    }
};
