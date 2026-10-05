# Rotate Array - Solution

## Problem Statement
Given an array, rotate the array to the right by k steps, where k is non-negative.

## Step-by-Step Logic

1. **Handle Overflow**:
   - Normalize k using modulo operation to handle cases where k > array size
   - `k = k % n` ensures k is within valid range

2. **Three-Step Reversal**:
   - **Step 1**: Reverse first n-k elements
   - **Step 2**: Reverse remaining k elements  
   - **Step 3**: Reverse entire array

3. **Mathematical Insight**:
   - This approach efficiently rotates array in O(1) space
   - Based on reversal properties and array partitioning

## Complexity Analysis

### Time Complexity: **O(n)**
- Three reverse operations, each taking O(n) time
- Total: O(3n) = O(n)

### Space Complexity: **O(1)**
- In-place operations using reverse function
- No additional data structures used
- Only constant extra space for variables

## Final Code with Comments

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        // Normalize k to handle cases where k > n
        k = k % n;
        
        // Step 1: Reverse first n-k elements
        reverse(nums.begin(), nums.begin() + (n - k));

        // Step 2: Reverse remaining k elements
        reverse(nums.begin() + (n - k), nums.end());
    
        // Step 3: Reverse entire array to get final result
        reverse(nums.begin(), nums.end());
    }
};
