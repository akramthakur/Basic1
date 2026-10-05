# Fibonacci Number - Solution

## Problem Statement
The Fibonacci numbers, commonly denoted `F(n)` form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from `0` and `1`. Given `n`, calculate `F(n)`.

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **Base Cases**: 
   - `F(0) = 0`
   - `F(1) = 1`
2. **Recurrence Relation**: `F(n) = F(n-1) + F(n-2)` for `n ≥ 2`
3. **Bottom-up Computation**: Fill DP array from smallest to largest subproblems
4. **Return Result**: Value at `dp[n]` is the nth Fibonacci number

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through 2 to n
- **O(1)** operations per iteration

### Space Complexity: **O(n)**
- **O(n)** for DP array storage
- Can be optimized to **O(1)** by storing only last two values

## Final Code with Comments

```cpp
class Solution {
public:
    int fib(int n) {
        // Handle base cases
        if(n == 0) return 0;
        if(n == 1) return 1;
        
        // DP array to store Fibonacci numbers
        vector<int> dp(n + 1);
        
        // Initialize base cases
        dp[0] = 0;
        dp[1] = 1;
        
        // Fill DP array using recurrence relation
        for(int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
};
