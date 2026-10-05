# Missing Number - Solution

## Problem Statement
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

## Step-by-Step Logic

### Algorithm:
1. **XOR Properties**: Use bitwise XOR to find the missing number
2. **Two-Pass Approach**:
   - First pass: XOR all numbers from 1 to n
   - Second pass: XOR all numbers in the array
3. **Cancellation Effect**: All present numbers cancel out, leaving only the missing number

### Key Insight:
- XOR is commutative and associative: a ^ b ^ a = b
- XORing a number with itself results in 0
- The missing number will be the only one that doesn't cancel out

## Complexity Analysis

### Time Complexity: **O(n)**
- Two passes through the array/range
- Constant time XOR operations

### Space Complexity: **O(1)**
- Only one variable used regardless of input size

## Final Code with Comments

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int ans = 0;
        int n = nums.size();
        
        // XOR all numbers from 1 to n
        for(int i = 1; i <= n; i++) {
            ans ^= i;
        }
        
        // XOR all numbers in the array
        // This cancels out all numbers that are present
        for(int i = 0; i < nums.size(); i++) {
            ans ^= nums[i];
        }
        
        return ans;  // The remaining number is the missing one
    }
};
