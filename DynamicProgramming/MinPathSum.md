# Minimum Path Sum - Solution

## Problem Statement
Given an `m x n` grid filled with non-negative numbers, find a path from top-left to bottom-right which minimizes the sum of all numbers along its path. The robot can only move either down or right at any point in time.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to compute minimum path sum
2. **State Definition**: `dp[i][j]` = minimum path sum to reach cell (i,j)
3. **Recurrence Relation**: 
   - `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`
   - Current cell value + minimum of path from above or left
4. **Base Cases**: 
   - First row: cumulative sum from left
   - First column: cumulative sum from above

### Key Insight:
- Each cell's minimum path depends only on its top and left neighbors
- First row and first column have only one possible path (straight line)
- We build the solution incrementally from start to end

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
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        
        // Create DP table
        vector<vector<int>> dp(m, vector<int>(n, 0));
        
        // Initialize starting point
        dp[0][0] = grid[0][0];
        
        // Initialize first column: only path is straight down
        for (int i = 1; i < m; i++) {
            dp[i][0] = grid[i][0] + dp[i - 1][0];
        }
        
        // Initialize first row: only path is straight right
        for (int j = 1; j < n; j++) {
            dp[0][j] = grid[0][j] + dp[0][j - 1];
        }
        
        // Fill DP table for remaining cells
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                // Current cell value + minimum of path from above or left
                dp[i][j] = grid[i][j] + min(dp[i - 1][j], dp[i][j - 1]);
            }
        }
        
        return dp[m - 1][n - 1];
    }
};
