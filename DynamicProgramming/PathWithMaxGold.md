# Path with Maximum Gold - Solution

## Problem Statement
Given a 2D grid `grid` where each cell may contain gold (positive integer) or be empty (0), find the maximum amount of gold you can collect by:
- Starting from any cell containing gold
- Moving to adjacent cells (up, down, left, right) that contain gold
- Cannot visit the same cell more than once in the same path
- Cannot visit cells with 0 gold

## Step-by-Step Logic

### Algorithm:
1. **DFS with Backtracking**: Explore all possible paths from each gold-containing cell
2. **Movement Constraints**: From any cell (i,j), can move to 4 directions (up, down, left, right)
3. **Backtracking**: Mark cell as visited during exploration, restore after
4. **Multiple Starting Points**: Try all gold-containing cells as starting positions

### Key Insight:
- This is an exhaustive search problem with path constraints
- At each step, we have up to four possible moves
- Must use backtracking to explore all paths without modifying original grid

## Complexity Analysis

### Time Complexity: **O((n × m) × 4^k)**
- Where k is the maximum path length (number of gold cells)
- In worst case, exponential but constrained by gold distribution

### Space Complexity: **O(n × m)**
- Recursion stack depth: O(k) where k is path length
- No extra DP table needed due to backtracking

## Final Code with Comments

```cpp
class Solution {
public:
    // Direction vectors: down, up, left, right
    vector<int> roww = {1, -1, 0, 0};
    vector<int> coll = {0, 0, -1, 1};
    
    int dfs(vector<vector<int>> &grid, vector<vector<int>> &dp, int i, int j, int n, int m) {
        // Base cases: out of bounds or no gold
        if (i >= n || j >= m || i < 0 || j < 0 || grid[i][j] == 0)
            return 0;
        
        // Store current gold and mark as visited
        int cur = grid[i][j];
        grid[i][j] = 0;  // Mark visited
        
        int localMax = cur;  // Start with current cell's gold
        
        // Explore all four directions
        for (int k = 0; k < 4; k++) {
            int x = i + roww[k];
            int y = j + coll[k];
            localMax = max(localMax, cur + dfs(grid, dp, x, y, n, m));
        }
        
        // Backtrack: restore original value
        grid[i][j] = cur;
        
        return localMax;
    }
    
    int getMaximumGold(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        int maxGold = 0;
        
        // DP table (though not effectively used in this implementation)
        vector<vector<int>> dp(n, vector<int>(m, -1));
        
        // Try every cell as starting point
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // Only start from cells with gold
                if (grid[i][j] != 0) {
                    maxGold = max(maxGold, dfs(grid, dp, i, j, n, m));
                }
            }
        }
        
        return maxGold;
    }
};
