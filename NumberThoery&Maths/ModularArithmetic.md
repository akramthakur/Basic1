# Smallest Integer Divisible by K - Solution

## Problem Statement
Given a positive integer `k`, find the length of the smallest positive integer `n` such that `n` is divisible by `k`. The integer `n` must consist only of the digit 1 (like 1, 11, 111, 1111, etc.).

## Step-by-Step Logic

### Algorithm:
1. **Modular Arithmetic**: Track remainder as we build the number digit by digit
2. **Iterative Construction**: Build numbers of form 1, 11, 111, 1111... 
3. **Remainder Tracking**: Use the property: `new_remainder = (old_remainder * 10 + 1) % k`
4. **Early Termination**: If remainder becomes 0, return current length. If no solution found in k steps, return -1.

### Key Insight:
- If no solution found in k steps, there's a repeated remainder (by Pigeonhole Principle)
- Numbers grow as: 1, 11, 111, 1111... which can be built iteratively

## Complexity Analysis

### Time Complexity: **O(k)**
- In worst case, we check up to k different remainders
- Each step does constant time operations

### Space Complexity: **O(1)**
- Only a few integer variables used

## Final Code with Comments

```cpp
class Solution {
public:
    int smallestRepunitDivByK(int k) {
        // If k is even or divisible by 5, no solution exists
        // because numbers ending with 1 can't be divisible by 2 or 5
        if (k % 2 == 0 || k % 5 == 0) {
            return -1;
        }
        
        int remainder = 0;
        
        // Try up to k iterations (by Pigeonhole Principle)
        for (int length = 1; length <= k; length++) {
            // Build number iteratively: r = (r * 10 + 1) % k
            remainder = (remainder * 10 + 1) % k;
            
            // If remainder becomes 0, we found our answer
            if (remainder == 0) {
                return length;
            }
        }
        
        return -1;  // No solution found within k steps
    }
};
