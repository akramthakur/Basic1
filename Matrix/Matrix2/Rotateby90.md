# Rotate Image - Solution

## Problem Statement
You are given an n x n 2D matrix representing an image. Rotate the image by 90 degrees clockwise in-place.

## Step-by-Step Logic

1. **Transpose the Matrix**:
   - Swap elements across the main diagonal
   - `matrix[i][j]` becomes `matrix[j][i]`
   - Only process upper triangle to avoid double swapping

2. **Reverse Each Row**:
   - After transpose, reverse each row horizontally
   - This completes the 90-degree clockwise rotation

## Mathematical Insight
90° clockwise rotation = Transpose + Reverse rows

## Complexity Analysis

### Time Complexity: **O(n²)**
- Transpose operation: O(n²)
- Reverse rows: O(n²)
- Total: O(2n²) = O(n²)

### Space Complexity: **O(1)**
- In-place operations using swap and reverse
- No additional data structures used
- Only constant extra space for loop variables

## Final Code with Comments

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        
        // Step 1: Transpose the matrix (swap across main diagonal)
        for(int i = 0; i < n - 1; i++) {
            for(int j = i + 1; j < n; j++) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        
        // Step 2: Reverse each row to complete 90° rotation
        for(int i = 0; i < n; i++) {
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};
