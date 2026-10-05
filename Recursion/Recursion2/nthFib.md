# Nth Fibonacci Number - Solution

## Problem Statement
Calculate the nth Fibonacci number using recursion. The Fibonacci sequence is defined as:
- F(0) = 0
- F(1) = 1  
- F(n) = F(n-1) + F(n-2) for n > 1

## Step-by-Step Logic

1. **Base Cases**:
   - If n = 0, return 0
   - If n = 1, return 1

2. **Recursive Relation**:
   - For n > 1, return sum of previous two Fibonacci numbers
   - F(n) = F(n-1) + F(n-2)

3. **Tree Recursion**:
   - Each call branches into two recursive calls
   - Computes values by breaking down into smaller subproblems

## Complexity Analysis

### Time Complexity: **O(2^n)**
- Exponential time due to repeated calculations
- Each call generates 2 more calls
- For n=5: 15 calls, n=10: 177 calls, n=20: 21,891 calls

### Space Complexity: **O(n)**
- Maximum recursion depth is n
- Call stack grows linearly with n

## Final Code with Comments

```cpp
class Solution {
public:
    int nthFibonacci(int n) {
        // Base cases: F(0) = 0, F(1) = 1
        if(n == 0 || n == 1) {
            return n;
        }
        // Recursive case: F(n) = F(n-1) + F(n-2)
        return nthFibonacci(n - 1) + nthFibonacci(n - 2);
    }
};
