# Check K-th Bit - Solution

## Problem Statement
Given a number `n` and a position `k`, check if the k-th bit (0-based indexing from right) is set (1) or not (0).

## Step-by-Step Logic

### Algorithm:
1. **Create Bitmask**: Generate a number with only the k-th bit set
2. **Bitwise AND**: Perform AND operation between `n` and the bitmask
3. **Check Result**: If result is non-zero, k-th bit is set; otherwise, it's not set

### Key Operations:
- **Bitmask Creation**: `1 << k` creates a number with 1 at k-th position
- **Bitwise AND**: `n & mask` isolates the k-th bit
- **Zero Check**: Compare result with 0 to determine bit status

## Complexity Analysis

### Time Complexity: **O(1)**
- Constant time operations regardless of input size

### Space Complexity: **O(1)**
- No extra space used

## Final Code with Comments

```cpp
class Solution {
  public:
    bool checkKthBit(int n, int k) {
        // Create a mask with 1 at k-th position
        // 1 << k = 2^k (only k-th bit is 1)
        int mask = 1 << k;
        
        // Perform bitwise AND
        // If k-th bit is 1, result will be non-zero
        // If k-th bit is 0, result will be zero
        return (n & mask) != 0;
    }
};
