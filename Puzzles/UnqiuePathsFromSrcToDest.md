# Unique Paths from source to distance - Solution

## Problem Statement
A robot is located at the top-left corner of an `m × n` grid. The robot can only move either down or right at any point in time. The grid contains obstacles marked as `1` and empty spaces marked as `0`. Find the number of unique paths from top-left to bottom-right corner.

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **State Definition**: `dp[i][j]` = number of unique paths to reach cell `(i,j)`
2. **Obstacle Handling**: If cell has obstacle, paths through it = 0
3. **Base Cases**: 
   - First row: paths stop at first obstacle
   - First column: paths stop at first obstacle
4. **Recurrence Relation**: `dp[i][j] = dp[i-1][j] + dp[i][j-1]` (if no obstacle)

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Fill DP table with m × n cells
- Constant time operations per cell

### Space Complexity: **O(m × n)**
- DP table of size m × n
- Can be optimized to O(n)

## Final Code with Comments

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        
        // Create DP table
        vector<vector<int>> dp(m, vector<int>(n, 0));
        
        // Check if start or end cell has obstacle
        if (obstacleGrid[m-1][n-1] == 1 || obstacleGrid[0][0] == 1) {
            return 0;
        }
        
        // Initialize first column
        for (int i = 0; i < m; i++) {
            // If obstacle found, all subsequent cells in column are unreachable
            if (obstacleGrid[i][0] == 1) {
                dp[i][0] = 0;
                break;  // No paths beyond obstacle in first column
            }
            dp[i][0] = 1;
        }
        
        // Initialize first row
        for (int j = 0; j < n; j++) {
            // If obstacle found, all subsequent cells in row are unreachable
            if (obstacleGrid[0][j] == 1) {
                dp[0][j] = 0;
                break;  // No paths beyond obstacle in first row
            }
            dp[0][j] = 1;
        }
        
        // Fill DP table for remaining cells
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (obstacleGrid[i][j] == 1) {
                    dp[i][j] = 0;  // Obstacle blocks all paths
                } else {
                    // Paths to (i,j) = paths from above + paths from left
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        
        return dp[m-1][n-1];
    }
};
