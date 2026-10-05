# Toggle Bits in Range - Solution

## Problem Statement
Given a number `n` and a range `[l, r]` (1-based indexing), toggle all the bits in the given range (inclusive) and return the resulting number.

## Step-by-Step Logic

### Algorithm:
1. **Convert to 0-based indexing**: Since bit positions are typically 0-based
2. **Iterate through the range**: From left to right position
3. **Toggle each bit**: Use XOR operation with appropriate bitmask
4. **Return result**: Modified number after toggling all bits in range

### Key Operations:
- **Bitmask Creation**: `1 << position` creates a mask with 1 at target position
- **Toggle Operation**: `n ^ mask` flips the bit at target position
- **Range Handling**: Inclusive range from `l` to `r`

## Complexity Analysis

### Time Complexity: **O(r - l)**
- Linear in the size of the range
- Each bit in the range is processed once

### Space Complexity: **O(1)**
- Constant extra space used

## Final Code with Comments

```cpp
class Solution {
  public:
    int toggleBits(int n, int l, int r) {
        // Convert to 0-based indexing
        l--;
        r--;
        
        // Toggle each bit in the range [l, r]
        while (l <= r) {
            // Create mask with 1 at position l
            int mask = 1 << l;
            // Toggle the bit using XOR
            n = n ^ mask;
            l++;
        }
        return n;
    }
};
