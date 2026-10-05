# Running Sum of 1D Array - Solution

## Problem Statement
Given an array `nums`, return the running sum of the array. The running sum is calculated as `runningSum[i] = sum(nums[0]…nums[i])` for each position i.

## Step-by-Step Logic

1. **Initialize Result Array**:
   - Create output array of same size as input
   - First element is same as first input element

2. **Iterative Sum Calculation**:
   - For each position i, add current element to previous running sum
   - Use dynamic programming approach: current sum = previous sum + current element

3. **Return Result**:
   - Return the computed running sum array

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array: O(n)
- Each element processed exactly once

### Space Complexity: **O(n)**
- Output array of size n: O(n)
- Could be O(1) if modified in-place (but problem typically expects new array)

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int n = nums.size();
        // Create result array initialized with zeros
        vector<int> ans(n, 0);
        
        // First element remains the same
        ans[0] = nums[0];
        
        // Calculate running sum for remaining elements
        for(int i = 1; i < n; i++){
            // Current sum = previous sum + current element
            ans[i] = ans[i-1] + nums[i];
        }
        
        return ans;
    }
};
