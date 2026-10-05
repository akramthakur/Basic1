# Perfect Squares - Solution

## Problem Statement
Given an integer `n`, return the least number of perfect square numbers that sum to `n`.

A perfect square is an integer that is the square of an integer (e.g., 1, 4, 9, 16, ...).

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to compute minimum squares
2. **State Definition**: `dp[i]` = minimum number of perfect squares that sum to `i`
3. **Recurrence Relation**: For each `i`, try all perfect squares ≤ `i`
4. **Transition**: `dp[i] = min(dp[i], dp[i - s] + 1)` where `s` is a perfect square

### Key Insight:
- Every number can be represented as sum of perfect squares (Lagrange's Four Square Theorem)
- We need to find the minimum count using dynamic programming
- Try subtracting all possible perfect squares and take minimum

## Complexity Analysis

### Time Complexity: **O(n × √n)**
- Outer loop: O(n) for numbers 1 to n
- Inner loop: O(√n) for perfect squares up to i
- Total: O(n × √n)

### Space Complexity: **O(n)**
- DP array of size n+1

## Final Code with Comments

```cpp
class Solution {
public:
    int numSquares(int n) {
        // Initialize DP array with maximum values
        vector<int> dp(n + 1, INT_MAX);
        
        // Base case: 0 can be represented with 0 squares
        dp[0] = 0;
        
        // Fill DP table from 1 to n
        for (int i = 1; i <= n; i++) {
            // Try all perfect squares less than or equal to i
            for (int j = 1; j * j <= i; j++) {
                int square = j * j;
                
                // Update minimum count
                dp[i] = min(dp[i], dp[i - square] + 1);
            }
        }
        
        return dp[n];
    }
};
