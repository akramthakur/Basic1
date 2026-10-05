# Set Matrix Zeroes - Solution

## Problem Statement
Given an `m x n` matrix, if an element is 0, set its entire row and column to 0. Do it in-place.

## Step-by-Step Logic

### Two-Pass Approach:
1. **First Pass**: Scan entire matrix and store coordinates of all zero elements
2. **Second Pass**: For each stored zero coordinate, set entire row and column to zero
3. **In-place Modification**: Directly modify the input matrix

## Complexity Analysis

### Time Complexity: **O(m × n × (m + n))**
- **O(m × n)** for scanning matrix to find zeros
- **O(k × (m + n))** for setting rows/columns to zero (k = number of zeros)
- **m** = number of rows, **n** = number of columns

### Space Complexity: **O(k)**
- **O(k)** for storing zero coordinates (k = number of zeros)
- **Worst Case**: O(m × n) when all elements are zero

## Final Code with Comments

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        // Store coordinates of all zero elements
        vector<pair<int, int>> zeroPositions;
        
        // First pass: Find all zero positions
        for(int i = 0; i < matrix.size(); i++) {
            for(int j = 0; j < matrix[i].size(); j++) {
                if(matrix[i][j] == 0) {
                    zeroPositions.push_back({i, j});
                }
            }
        }
        
        // Second pass: Set entire rows and columns to zero
        for(auto &p : zeroPositions) {
            int row = p.first;
            int col = p.second;
            
            // Set entire column to zero
            for(int i = 0; i < matrix.size(); i++) {
                matrix[i][col] = 0;
            }
            
            // Set entire row to zero
            for(int j = 0; j < matrix[row].size(); j++) {
                matrix[row][j] = 0;
            }
        }
    }
};
