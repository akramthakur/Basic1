# Rat in Maze - Longest Path Finder

## Problem Statement
Given an N×N maze where `1` represents valid paths and `0` represents obstacles, find the longest path from the top-left corner (0,0) to the bottom-right corner (N-1,N-1) using movements: Down (D), Up (U), Right (R), Left (L).

## Solution Approach

### Backtracking with Path Tracking:
1. **DFS Exploration**: Systematically explore all possible paths
2. **Path Recording**: Track movement directions in a string
3. **Longest Path Selection**: Compare path lengths to find maximum

## Final Code

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
        
        // Explore DOWN direction
        if(row != n-1 && maze[row+1][col] != 0 && !vis[row+1][col]) {
            vis[row][col] = 1;
            temp += 'D';
            findPath(ans, temp, maze, row+1, col, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        // Explore UP direction  
        if(row != 0 && maze[row-1][col] != 0 && !vis[row-1][col]) {
            vis[row][col] = 1;
            temp += 'U';
            findPath(ans, temp, maze, row-1, col, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        // Explore RIGHT direction
        if(col != n-1 && maze[row][col+1] != 0 && !vis[row][col+1]) {
            vis[row][col] = 1;
            temp += 'R';
            findPath(ans, temp, maze, row, col+1, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
        
        // Explore LEFT direction
        if(col != 0 && maze[row][col-1] != 0 && !vis[row][col-1]) {
            vis[row][col] = 1;
            temp += 'L';
            findPath(ans, temp, maze, row, col-1, n, vis);
            vis[row][col] = 0;
            temp.pop_back();
        }
    }
    
    string ratInMazeLongestPath(vector<vector<int>>& maze) {
        int n = maze.size();
        vector<string> ans;
        string temp;
        vector<vector<int>> vis(n, vector<int>(n, 0));
        
        // Generate all possible paths
        findPath(ans, temp, maze, 0, 0, n, vis);
        
        // Sort paths lexicographically
        sort(ans.begin(), ans.end());
        
        // Find path with maximum length
        pair<int, string> k = {0, ""};
        for(int i = 0; i < ans.size(); i++) {
            if(k.first < ans[i].length()) {
                k = {ans[i].length(), ans[i]};
            }
        }
        
        return k.second;
    }
};
