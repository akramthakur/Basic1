# Unique Binary Search Trees - Solution

## Problem Statement
Given an integer `n`, return the number of structurally unique BSTs (binary search trees) that store values `1` to `n`.

## Step-by-Step Logic

### Dynamic Programming with Catalan Number Formula:
1. **Base Case**: Empty tree counts as 1 unique BST
2. **Catalan Number**: The solution follows Catalan number sequence
3. **Recurrence Relation**: 
   - For n nodes, sum over all possible root positions
   - C(n) = Σ [C(i-1) × C(n-i)] for i from 1 to n
4. **Optimized Formula**: Use direct Catalan number formula for O(n) time

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through 1 to n
- **O(1)** operations per iteration

### Space Complexity: **O(n)**
- **O(n)** for DP array storage
- Can be optimized to **O(1)** with single variable

## Final Code with Comments

```cpp
class Solution {
public:
    int numTrees(int n) {
        // DP array to store Catalan numbers
        vector<double> dp(n + 1);
        
        // Base case: empty tree
        dp[0] = 1;
        
        // Calculate Catalan numbers using recurrence relation
        for(int i = 1; i <= n; i++) {
            // Catalan number formula: C(n) = (2(2n-1)/(n+1)) * C(n-1)
            dp[i] = ((2.0 * (2 * i - 1)) / (i + 1)) * dp[i - 1];
        }
        
        // Return the nth Catalan number
        return (int)dp[n];
    }
};
