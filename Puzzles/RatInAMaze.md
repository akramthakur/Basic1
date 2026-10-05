# Rat in a Maze - Solution

## Problem Statement
Given an N×N maze where `1` represents valid paths and `0` represents obstacles, find all possible paths for a rat to go from the top-left corner (0,0) to the bottom-right corner (N-1,N-1). The rat can move in four directions: Up, Down, Left, Right.

## Step-by-Step Logic

### Backtracking Approach:
1. **Base Case**: When rat reaches destination (n-1, n-1), save current path
2. **Movement Constraints**: Check bounds, obstacles, and visited cells
3. **Path Tracking**: Build path string with directions ('D', 'U', 'R', 'L')
4. **Backtracking**: Mark/unmark visited cells and update path string

## Algorithm Details

### Movement Directions:
- **Down**: (row+1, col) → 'D'
- **Up**: (row-1, col) → 'U'  
- **Right**: (row, col+1) → 'R'
- **Left**: (row, col-1) → 'L'

### Constraints Checking:
- **Bounds**: row and col between 0 and n-1
- **Obstacles**: maze[row][col] != 0
- **Visited**: !vis[row][col] (avoid cycles)

### Backtracking Steps:
1. Mark current cell as visited
2. Append direction to path
3. Recursively explore chosen direction
4. Unmark current cell (backtrack)
5. Remove direction from path

## Complexity Analysis

### Time Complexity: **O(4^(n²))**
- In worst case, explore all 4 directions at each cell
- Theoretical upper bound: O(4^(n²))
- Practical: Much less due to constraints

### Space Complexity: **O(n²)**
- Visited matrix: O(n²)
- Recursion stack: O(n²)
- Output storage: O(paths × path_length)

## Final Code with Comments

```cpp
class Solution {
public:
    void findPath(vector<string>& ans, string& temp, vector<vector<int>>& maze, 
                 int row, int col, int n, vector<vector<int>>& vis) {
        
        // Base case: reached destination
        if(row == n-1 && col == n-1) {
            ans.push_back(temp);
            return;
        }
        
        // Move DOWN: row+1, col
        if(row != n-1 && maze[row+1][col] != 0 && !vis[row+1][col]) {
            vis[row][col] = 1;        // Mark current cell visited
            temp += 'D';              // Add direction to path
            findPath(ans, temp, maze, row+1, col, n, vis);  // Recurse
            vis[row][col] = 0;        // Backtrack: unmark
            temp.pop_back();          // Backtrack: remove direction
        }
        
        // Move UP: row-1, col
        if(row != 0 && maze[row-1][col] != 0 && !vis[row-1][col]) {
            vis[row][col] = 1;
            temp += 'U';
            findPath(ans, temp, maze, row-1, col, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        // Move RIGHT: row, col+1
        if(col != n-1 && maze[row][col+1] != 0 && !vis[row][col+1]) {
            vis[row][col] = 1;
            temp += 'R';
            findPath(ans, temp, maze, row, col+1, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        // Move LEFT: row, col-1
        if(col != 0 && maze[row][col-1] != 0 && !vis[row][col-1]) {
            vis[row][col] = 1;
            temp += 'L';
            findPath(ans, temp, maze, row, col-1, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        return;
    }
    
    vector<string> ratInMaze(vector<vector<int>>& maze) {
        int n = maze.size();
        vector<string> ans;
        string temp;
        vector<vector<int>> vis(n, vector<int>(n, 0));
        
        // Start DFS from (0,0) if starting cell is valid
        if(maze[0][0] != 0) {
            findPath(ans, temp, maze, 0, 0, n, vis);
        }
        
        // Return paths in lexicographical order
        sort(ans.begin(), ans.end());
        return ans;
    }
};
