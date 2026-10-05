# Flood Fill - Solution

## Problem Statement
Given an `m x n` image represented by a 2D integer array where `image[i][j]` represents the pixel value, and given the starting pixel `(sr, sc)` and a new color `color`, perform a flood fill starting from the starting pixel and return the modified image.

A flood fill changes the color of all connected pixels (4-directionally) that have the same starting color to the new color.

## Step-by-Step Logic

### DFS Recursive Approach:
1. **Base Case Checks**:
   - Out of bounds
   - Pixel already has new color
   - Pixel has different color than starting pixel
2. **Color Update**: Change current pixel to new color
3. **Recursive Calls**: Explore 4-directional neighbors (up, down, left, right)
4. **Return Image**: Modified image after flood fill

## Complexity Analysis

### Time Complexity: **O(m × n)**
- **O(m × n)** in worst case when entire image needs to be filled
- Each pixel is visited at most once
- **m** = number of rows, **n** = number of columns

### Space Complexity: **O(m × n)**
- **O(m × n)** for recursion stack in worst case
- In worst case, recursion depth equals number of pixels in connected component

## Final Code with Comments

```cpp
class Solution {
public:
    void dfs(vector<vector<int>> &image, int i, int j, int val, int color) {
        // Base cases:
        // 1. Out of bounds
        // 2. Pixel already has new color (prevents infinite recursion)
        // 3. Pixel has different color than starting pixel
        if(i < 0 || i >= image.size() || j < 0 || j >= image[0].size() || 
           image[i][j] == color || image[i][j] != val) {
            return;
        }
        
        // Update current pixel to new color
        image[i][j] = color;
        
        // Recursively flood fill 4-directional neighbors
        dfs(image, i - 1, j, val, color);  // Up
        dfs(image, i + 1, j, val, color);  // Down
        dfs(image, i, j - 1, val, color);  // Left
        dfs(image, i, j + 1, val, color);  // Right
    }
    
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int val = image[sr][sc];  // Store original color of starting pixel
        
        // If starting color is same as new color, no need to do anything
        if(val != color) {
            dfs(image, sr, sc, val, color);
        }
        
        return image;
    }
};
