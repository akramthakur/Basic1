# Power of Two - Solution

## Problem Statement
Given an integer `n`, determine if it is a power of two.

## Step-by-Step Logic

### Algorithm:
1. **Positive Check**: Ensure number is positive (powers of two are always positive)
2. **Bit Pattern Check**: Use the property that powers of two have exactly one '1' bit
3. **Bit Trick**: `n & (n-1)` removes the rightmost '1' bit. For powers of two, this results in 0.

### Key Insight:
- **Powers of two in binary**: 1, 10, 100, 1000, 10000, ...
- **n & (n-1) trick**: 
  - If n has exactly one '1' bit, then n & (n-1) = 0
  - If n has more than one '1' bit, then n & (n-1) ≠ 0

## Complexity Analysis

### Time Complexity: **O(1)**
- Constant time bitwise operations

### Space Complexity: **O(1)**
- No extra space used

## Final Code with Comments

```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        // Check: 
        // 1. n > 0 (powers of two are positive)
        // 2. n & (n-1) == 0 (only one '1' bit in binary representation)
        return (n > 0) && !(n & (n - 1));
    }
};
