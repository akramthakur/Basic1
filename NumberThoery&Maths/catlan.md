# Unique Binary Search Trees - Solution

## Problem Statement
Given an integer `n`, return the number of structurally unique BSTs (binary search trees) that can be formed with `n` distinct nodes.

## Step-by-Step Logic

### Algorithm:
1. **Catalan Numbers**: The number of unique BSTs follows the Catalan number sequence
2. **Dynamic Programming**: Use the recurrence relation for Catalan numbers
3. **Closed Form**: Use the formula: C(n) = (2n choose n) / (n + 1)

### Key Insight:
- For n nodes, the number of unique BSTs is the nth Catalan number
- Catalan numbers satisfy: C(n) = Σ [C(i) × C(n-i-1)] for i = 0 to n-1
- Direct formula: C(n) = (2n)! / (n! × (n+1)!)

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass from 1 to n
- Constant time operations per step

### Space Complexity: **O(n)**
- DP array of size n+1

## Final Code with Comments

```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<double> dp(n + 1);
        dp[0] = 1;  // Base case: empty tree
        
        for (int i = 1; i <= n; i++) {
            // Catalan number recurrence: 
            // C(n) = (2(2n-1) / (n+1)) * C(n-1)
            dp[i] = ((2.0 * (2 * i - 1)) / (i + 1)) * dp[i - 1];
        }
        
        return (int)dp[n];
    }
};
