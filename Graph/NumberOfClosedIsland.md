# Number of Closed Islands - Solution

## Problem Statement
Given a 2D grid consisting of 0s (land) and 1s (water), a closed island is a group of 0s completely surrounded by 1s (water). Return the number of closed islands in the grid.

## Step-by-Step Logic

### Algorithm:
1. **DFS Flood Fill**: Use DFS to explore connected land cells (0s)
2. **Boundary Check**: If DFS reaches grid boundary, it's not a closed island
3. **Mark Visited**: Convert visited land to water to avoid recounting
4. **Validation**: An island is closed only if DFS doesn't reach boundaries

### Key Insight:
- Closed islands must not touch grid boundaries
- We can use DFS to explore islands and check if they're surrounded
- Convert visited cells to water (1) to mark them as processed

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Each cell visited at most once
- DFS runs in O(1) per cell after marking

### Space Complexity: **O(m × n)**
- Recursion stack in worst case (when entire grid is land)
- Could be O(min(m, n)) with iterative DFS

## Final Code with Comments

```cpp
class Solution {
public:
    int closedIsland(vector<vector<int>>& grid) {
        int res = 0;
        // Iterate through all cells
        for(int i = 0; i < grid.size(); i++) {
            for(int j = 0; j < grid[0].size(); j++) {
                // Found unvisited land
                if(grid[i][j] == 0) {
                    // DFS returns true if island is closed
                    res += dfs(grid, i, j) ? 1 : 0;
                }
            }
        }
        return res;
    }
    
    bool dfs(vector<vector<int>>& g, int i, int j) {
        // If out of bounds, reached boundary - not closed
        if(i < 0 || j < 0 || i >= g.size() || j >= g[i].size()) {
            return false;
        }
        
        // If water or already visited, return true (boundary not reached from here)
        if(g[i][j] == 1) {
            return true;
        }
        
        // Mark current cell as visited (convert to water)
        g[i][j] = 1;
        
        // Explore all 4 directions
        bool down = dfs(g, i + 1, j);
        bool right = dfs(g, i, j + 1);
        bool up = dfs(g, i - 1, j);
        bool left = dfs(g, i, j - 1);
        
        // Island is closed only if ALL directions don't reach boundary
        return down && right && up && left;
    }
};
