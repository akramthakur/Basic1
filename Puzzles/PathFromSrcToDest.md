# Unique Paths - Solution

## Problem Statement
A robot is located at the top-left corner of an `m x n` grid. The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

How many possible unique paths are there?

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to count paths
2. **State Definition**: `dp[i][j]` = number of unique paths to reach cell (i,j)
3. **Recurrence Relation**: 
   - `dp[i][j] = dp[i-1][j] + dp[i][j-1]`
   - Paths to (i,j) = paths from above + paths from left
4. **Base Cases**: First row and first column have only 1 path each

### Key Insight:
- Robot can only move down or right
- Each cell's path count depends on its top and left neighbors
- First row and column have only one possible path (straight line)

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Fill DP table with m × n cells
- Constant time operations per cell

### Space Complexity: **O(m × n)**
- DP table of size m × n
- Can be optimized to O(n) or O(min(m,n))

## Final Code with Comments

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        // Create DP table
        vector<vector<int>> dp(m, vector<int>(n, 0));
        
        // Initialize first column: only one path (straight down)
        for (int i = 0; i < m; i++) {
            dp[i][0] = 1;
        }
        
        // Initialize first row: only one path (straight right)
        for (int j = 0; j < n; j++) {
            dp[0][j] = 1;
        }
        
        // Fill DP table
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                // Paths to (i,j) = paths from above + paths from left
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        
        return dp[m - 1][n - 1];
    }
};
