# Reverse Exponentiation - Solution

## Problem Statement
Given a number n, find the value of n raised to the power of its own reverse.

## Step-by-Step Logic

1. **Reverse Calculation**:
   - Extract digits from n using modulo and division
   - Build reversed number by adding digits in reverse order
   - Handle leading zeros automatically (e.g., 10 → 1)

2. **Recursive Power Calculation**:
   - Base case: when power reaches 0, return 1
   - Recursive case: multiply n with result of n^(power-1)
   - Continue until power reduces to 0

3. **Special Case Handling**:
   - Directly return 10 when n = 10 (reverse is 1)

## Complexity Analysis

### Time Complexity: **O(d + r)**
- **d**: Number of digits in n (for reversal) - O(d)
- **r**: Value of reversed number (for exponentiation) - O(r)
- Total: O(d + r)

### Space Complexity: **O(r)**
- Recursion stack depth equals the reversed number value
- Each recursive call uses stack space

## Final Code with Comments

```cpp
class Solution {
public:
    // Recursive power function
    int rec(int n, int power) {
        // Base case: anything to power 0 is 1
        if(power == 0) {
            return 1;
        }
        // Recursive case: n^power = n * n^(power-1)
        return n * rec(n, power - 1);
    }
  
    int reverseExponentiation(int n) {
        // Special case: n=10 has reverse 1
        if(n == 10) {
            return 10;
        }
        
        // Calculate reverse of n
        int reverse = 0;
        int temp = n;
        while(temp > 0) {
            reverse = reverse * 10 + (temp % 10);  // Add last digit
            temp = temp / 10;                      // Remove last digit
        }
        
        // Calculate n^reverse using recursion
        int ans = rec(n, reverse);
        return ans;
    }
};
