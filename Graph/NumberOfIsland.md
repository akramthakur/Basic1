# Number of Islands - Solution

## Problem Statement
Given an `m x n` 2D binary grid which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

## Step-by-Step Logic

### BFS Approach for Connected Components:
1. **Grid Traversal**: Iterate through each cell in the grid
2. **Island Discovery**: When unvisited land (`'1'`) is found:
   - Increment island counter
   - Perform BFS to mark entire island
3. **BFS Expansion**: 
   - Use 4-directional movement (up, right, down, left)
   - Mark visited cells to avoid reprocessing
   - Only traverse adjacent land cells
4. **Return Count**: Total number of islands discovered

## Complexity Analysis

### Time Complexity: **O(m × n)**
- **O(m × n)** for visiting each cell once
- **O(m × n)** for BFS in worst case (single large island)
- **m** = number of rows, **n** = number of columns

### Space Complexity: **O(m × n)**
- **O(m × n)** for visited matrix
- **O(min(m, n))** for BFS queue in worst case
- Can be optimized to **O(1)** by modifying input grid

## Final Code with Comments

```cpp
class Solution {
public:
    void bfs(int row, int col, vector<vector<int>>& vis, vector<vector<char>>& grid) {
        // Mark starting cell as visited
        vis[row][col] = 1;
        
        // Queue for BFS traversal
        queue<pair<int, int>> q;
        q.push({row, col});
        
        int n = grid.size();     // Number of rows
        int m = grid[0].size();  // Number of columns
        
        // Process until queue is empty
        while(!q.empty()) {
            // Get current cell coordinates
            int row = q.front().first;
            int col = q.front().second;
            q.pop();
            
            // 4-directional movement: up, right, down, left
            int delrow[] = {-1, 0, 1, 0};
            int delcol[] = {0, 1, 0, -1};
            
            // Check all 4 neighbors
            for(int i = 0; i < 4; i++) {
                int nrow = row + delrow[i];  // New row
                int ncol = col + delcol[i];  // New column
                
                // Check if neighbor is within bounds, is land, and not visited
                if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m &&
                   grid[nrow][ncol] == '1' && !vis[nrow][ncol]) {
                    // Mark neighbor as visited and add to queue
                    vis[nrow][ncol] = 1;
                    q.push({nrow, ncol});
                }
            }
        }
    }
    
    int numIslands(vector<vector<char>>& grid) {
        int n = grid.size();     // Number of rows
        int m = grid[0].size();  // Number of columns
        
        // Visited matrix to track visited cells
        vector<vector<int>> vis(n, vector<int>(m, 0));
        int cnt = 0;  // Island counter
        
        // Iterate through all cells in the grid
        for(int row = 0; row < n; row++) {
            for(int col = 0; col < m; col++) {
                // If cell is unvisited land, found new island
                if(!vis[row][col] && grid[row][col] == '1') {
                    cnt++;  // Increment island count
                    bfs(row, col, vis, grid);  // Mark entire island
                }
            }
        }
        
        return cnt;
    }
};
