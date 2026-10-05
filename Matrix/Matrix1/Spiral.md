# Spiral Matrix - Solution

## Problem Statement
Given an m x n matrix, return all elements of the matrix in spiral order.

## Step-by-Step Logic

1. **Four Pointer Approach**:
   - `left`, `right`: Track column boundaries
   - `top`, `bottom`: Track row boundaries
   - Shrink boundaries after processing each side

2. **Four-Step Spiral Traversal**:
   - **Left to Right**: Process top row
   - **Top to Bottom**: Process right column  
   - **Right to Left**: Process bottom row
   - **Bottom to Top**: Process left column

3. **Boundary Checks**:
   - Check `top <= bottom` before processing bottom row
   - Check `left <= right` before processing left column

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Visit each element exactly once
- m = number of rows, n = number of columns

### Space Complexity: **O(1)** excluding output
- Only constant extra space for pointers
- Output vector is O(m × n) but required by problem

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans;
        // Initialize boundaries
        int left = 0, right = matrix[0].size() - 1;
        int top = 0, bottom = matrix.size() - 1;

        // Continue while there are elements to process
        while(left <= right && top <= bottom) {
            // Step 1: Traverse from left to right (top row)
            for(int i = left; i <= right; i++) {
                ans.push_back(matrix[top][i]);
            }
            top++;  // Move top boundary down
            
            // Step 2: Traverse from top to bottom (right column)
            for(int i = top; i <= bottom; i++) {
                ans.push_back(matrix[i][right]);
            }
            right--;  // Move right boundary left
            
            // Step 3: Traverse from right to left (bottom row)
            // Check if there's still a row to process
            if(top <= bottom) {
                for(int i = right; i >= left; i--) {
                    ans.push_back(matrix[bottom][i]);
                }
                bottom--;  // Move bottom boundary up
            }
            
            // Step 4: Traverse from bottom to top (left column)
            // Check if there's still a column to process
            if(left <= right) {
                for(int i = bottom; i >= top; i--) {
                    ans.push_back(matrix[i][left]);
                }
                left++;  // Move left boundary right
            }
        }
        return ans;
    }
};
