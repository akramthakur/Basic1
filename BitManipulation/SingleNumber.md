# Single Number - Solution

## Problem Statement
Given a non-empty array of integers where every element appears twice except for one element which appears exactly once, find that single element.

## Step-by-Step Logic

### Algorithm:
1. **XOR Operation**: Use bitwise XOR to find the unique element
2. **XOR Properties**:
   - a ^ a = 0 (same numbers cancel out)
   - a ^ 0 = a (XOR with zero returns the number)
   - XOR is commutative and associative

### Key Insight:
- All duplicate numbers will cancel each other out (a ^ a = 0)
- The remaining number will be the single occurrence (a ^ 0 = a)

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array
- Constant time XOR operation per element

### Space Complexity: **O(1)**
- Only one variable used regardless of input size

## Final Code with Comments

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;
        
        // XOR all numbers in the array
        for(int i = 0; i < nums.size(); i++) {
            ans ^= nums[i];  // XOR operation
        }
        
        return ans;  // The remaining number is the single occurrence
    }
};
