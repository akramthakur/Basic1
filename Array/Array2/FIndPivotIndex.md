# Find Pivot Index - Solution

## Problem Statement
Given an array of integers, find the pivot index where the sum of all elements to the left equals the sum of all elements to the right. Return -1 if no such index exists.

## Step-by-Step Logic

1. **Calculate Total Sum**:
   - Compute sum of all elements in the array
   - This gives us the right sum for index 0

2. **Iterative Left Sum Tracking**:
   - Maintain running left sum as we iterate
   - Right sum = total sum - left sum - current element
   - Check if left sum equals right sum at each position

3. **Early Return**:
   - Return first pivot index found
   - Return -1 if no pivot exists

## Complexity Analysis

### Time Complexity: **O(n)**
- One pass to calculate total sum: O(n)
- One pass to find pivot index: O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(1)**
- Only using constant extra space for variables
- No additional data structures

## Final Code with Comments

```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        
        // Calculate total sum of array
        for(int i = 0; i < n; i++){
            sum += nums[i];
        }
       
        int ls = 0;  // Left sum accumulator
        int res = -1; // Default result if no pivot found
        
        // Check each index as potential pivot
        for(int i = 0; i < n; i++){
            // Check if left sum equals right sum
            // Right sum = total - left - current element
            if(ls == sum - ls - nums[i]){
                return i;  // Found pivot index
            }
            ls += nums[i];  // Update left sum for next iteration
        }
        return res;  // No pivot index found
    }
};
