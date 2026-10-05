# Super Pow - Solution

## Problem Statement
Calculate `a^b mod 1337` where `a` is an integer and `b` is a very large positive integer represented as an array of digits.

## Step-by-Step Logic

### Algorithm:
1. **Modular Exponentiation**: Use properties of modular arithmetic
2. **Divide and Conquer**: Break the exponent into smaller parts
3. **Mathematical Properties**:
   - `(x × y) mod m = [(x mod m) × (y mod m)] mod m`
   - `a^(m+n) mod k = [(a^m mod k) × (a^n mod k)] mod k`
   - `a^(10×x + y) = (a^x)^10 × a^y`

### Key Insight:
- For exponent array `[b1, b2, ..., bn]`, it represents number `b1×10^(n-1) + b2×10^(n-2) + ... + bn`
- Use recursion: `a^[b1...bn] = (a^[b1...b(n-1)])^10 × a^(bn) mod 1337`

## Complexity Analysis

### Time Complexity: **O(n)**
- Where n is the number of digits in b
- Each digit processed once with constant time operations

### Space Complexity: **O(n)**
- Recursion stack depth equals number of digits
- Could be O(1) with iterative approach

## Final Code with Comments

```cpp
class Solution {
public:
    int base = 1337;
    
    // Helper function: compute a^k mod base
    int powmod(int a, int k) {
        a %= base;  // Reduce base first
        int res = 1;
        for (int i = 0; i < k; i++) {
            res = (res * a) % base;
        }
        return res;
    }
    
    int superPow(int a, vector<int>& b) {
        // Base case: empty exponent array
        if (b.empty()) return 1;
        
        // Get the last digit and remove it from array
        int last = b.back();
        b.pop_back();
        
        // Recursive formula:
        // a^[b1...bn] = (a^[b1...b(n-1)])^10 × a^(last) mod base
        int part1 = powmod(superPow(a, b), 10);
        int part2 = powmod(a, last);
        
        return (part1 * part2) % base;
    }
};
