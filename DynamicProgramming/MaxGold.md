# Maximum Gold Collection - Solution

## Problem Statement
Given a 2D grid `mat` where each cell contains a certain amount of gold, find the maximum amount of gold that can be collected starting from any cell in the first column and moving to adjacent cells (right, right-up, right-down) until reaching the last column.

## Step-by-Step Logic

### Algorithm:
1. **DFS with Memoization**: Explore all possible paths from each starting position in first column
2. **Movement Constraints**: From any cell (i,j), can move to:
   - (i-1, j+1) - right-up
   - (i, j+1)   - right
   - (i+1, j+1) - right-down
3. **Memoization**: Store computed results to avoid recomputation
4. **Multiple Starting Points**: Try all cells in first column as starting positions

### Key Insight:
- This is a path optimization problem in a grid
- At each step, we have three possible moves (right-up, right, right-down)
- The goal is to maximize gold collection from first column to last column

## Complexity Analysis

### Time Complexity: **O(n × m)**
- Each cell is visited once due to memoization
- n × m states to compute

### Space Complexity: **O(n × m)**
- DP table of size n × m
- Recursion stack depth: O(m)

## Final Code with Comments

```cpp
class Solution {
  public:
    int rec(vector<vector<int>> &mat, vector<vector<int>> &dp, int i, int j, int n, int m) {
        // Base case: out of bounds
        if (i == n || j == m || i < 0 || j < 0)
            return 0;
        
        // Return cached result if available
        if (dp[i][j] != -1) {
            return dp[i][j];
        }
        
        // Explore all three possible moves
        int rightUp = rec(mat, dp, i - 1, j + 1, n, m);    // Move right-up
        int right = rec(mat, dp, i, j + 1, n, m);          // Move right
        int rightDown = rec(mat, dp, i + 1, j + 1, n, m);  // Move right-down
        
        // Current gold + maximum from possible moves
        return dp[i][j] = mat[i][j] + max(rightUp, max(right, rightDown));
    }
    
    int maxGold(vector<vector<int>>& mat) {
        int n = mat.size();
        int m = mat[0].size();
        
        // DP table for memoization
        vector<vector<int>> dp(n, vector<int>(m, -1));
        
        int ans = INT_MIN;
        
        // Try all starting positions in first column
        for (int i = 0; i < n; i++) {
            ans = max(ans, rec(mat, dp, i, 0, n, m));
        }
        
        return ans;
    }
};
