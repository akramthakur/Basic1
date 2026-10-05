# Maximum Product Subarray - Solution

## Problem Statement
Given an integer array, find the contiguous subarray within the array that has the largest product and return the product.

## Step-by-Step Logic

1. **Two Pass Approach**:
   - **Forward Pass**: Calculate maximum product from left to right
   - **Backward Pass**: Calculate maximum product from right to left
   - Track maximum product from both passes

2. **Handling Negative Numbers**:
   - Negative numbers can become positive when multiplied by another negative
   - Two passes ensure we catch maximum product in both directions
   - Reset product to 1 when encountering zero

3. **Key Insight**:
   - Maximum product can come from either direction due to negative numbers
   - Zero resets the product chain

## Complexity Analysis

### Time Complexity: **O(n)**
- Two passes through the array: O(2n) = O(n)
- Constant time operations for each element

### Space Complexity: **O(1)**
- Only using constant extra space for variables
- No additional data structures needed

## Final Code with Comments

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxpro = INT_MIN;  // Track maximum product
        int pro = 1;           // Running product
        
        // Forward pass (left to right)
        for(int i = 0; i < nums.size(); i++){
            pro *= nums[i];           // Multiply current element
            maxpro = max(maxpro, pro); // Update maximum product
            
            // Reset if product becomes zero
            if(pro == 0){
                pro = 1;  // Start fresh from next element
            }
        }
        
        pro = 1;  // Reset product for backward pass
        
        // Backward pass (right to left)
        for(int i = nums.size() - 1; i >= 0; i--){
            pro *= nums[i];           // Multiply current element
            maxpro = max(maxpro, pro); // Update maximum product
            
            // Reset if product becomes zero
            if(pro == 0){
                pro = 1;  // Start fresh from next element
            }
        }
        
        return maxpro;  // Return maximum product found
    }
};
