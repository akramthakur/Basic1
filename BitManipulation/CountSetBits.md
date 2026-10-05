# Count Total Set Bits - Solution

## Problem Statement
Given a positive integer `n`, count the total number of set bits (1s) in the binary representation of all numbers from 1 to `n`.

## Step-by-Step Logic

### Algorithm:
1. **Recursive Pattern Recognition**: 
   - Find the largest power of 2 ≤ n (say 2^x)
   - Count bits in three parts:
     - Bits from 0 to 2^x - 1 (pattern repeats)
     - MSB bits from 2^x to n
     - Recursively count bits from 0 to (n - 2^x)

2. **Mathematical Formula**:
   - Total bits = (x * 2^(x-1)) + (n - 2^x + 1) + countSetBits(n - 2^x)

### Key Components:
- **bitsTillPower**: Set bits in numbers 0 to (2^x - 1)
- **msbBits**: Set bits from the most significant bit position
- **rest**: Recursively count remaining numbers

## Complexity Analysis

### Time Complexity: **O(log n)**
- Each recursive call reduces `n` by half
- Logarithmic number of calls

### Space Complexity: **O(log n)**
- Recursion stack depth is logarithmic

## Final Code with Comments

```cpp
class Solution {
  public:
    int countSetBits(int n) {
        // Base case
        if (n == 0) return 0;
        
        // Find the largest power of 2 <= n
        int x = log2(n);  // highest power of 2 <= n

        // 1. Bits from 0 to (2^x - 1)
        // Pattern: x * 2^(x-1)
        int bitsTillPower = x * (1 << (x - 1));
        
        // 2. MSB bits from 2^x to n
        // Each number in this range has MSB set
        int msbBits = n - (1 << x) + 1;
        
        // 3. Recursively count bits in remaining part
        int rest = countSetBits(n - (1 << x));

        return bitsTillPower + msbBits + rest;
    }
};
