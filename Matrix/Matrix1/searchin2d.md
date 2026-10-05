# Search a 2D Matrix - Solution

## Problem Statement
Write an efficient algorithm that searches for a target value in an m x n matrix with the following properties:
- Integers in each row are sorted
- The first integer of each row is greater than the last integer of the previous row

## Step-by-Step Logic

1. **Two-Level Binary Search**:
   - **First Search**: Find the correct row using first column values
   - **Second Search**: Search within the identified row

2. **Row Selection**:
   - Use binary search on first column to find row where:
     - `matrix[row][0] <= target <= matrix[row][last]`
   - If no such row exists, target is not in matrix

3. **Column Search**:
   - Once correct row is found, perform binary search on that row
   - Standard binary search algorithm

## Complexity Analysis

### Time Complexity: **O(log m + log n)**
- Binary search to find correct row: O(log m)
- Binary search within row: O(log n)
- Total: O(log m + log n) = O(log(mn))

### Space Complexity: **O(log n)** for recursive BS
- Recursive binary search stack depth: O(log n)
- Could be O(1) with iterative binary search

## Final Code with Comments

```cpp
class Solution {
public:
    // Recursive binary search helper function
    bool binarysearch(vector<int> arr, int lo, int hi, int target) {
        // Base case: target not found
        if(lo > hi) {
            return false;
        }
        
        int mid = lo + (hi - lo) / 2;  // Avoid overflow
        
        if(arr[mid] == target) {
            return true;  // Target found
        } else if(arr[mid] > target) {
            // Search left half
            return binarysearch(arr, lo, mid - 1, target);
        } else {
            // Search right half
            return binarysearch(arr, mid + 1, hi, target);
        }
    }
    
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int hi = matrix.size() - 1;
        int cols = matrix[0].size() - 1;
        int lo = 0;
     
        // Binary search to find the correct row
        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            
            // Check if target is within current row's range
            if((matrix[mid][0] <= target) && (matrix[mid][cols] >= target)) {
                // Target potentially in this row, search within it
                return binarysearch(matrix[mid], 0, cols, target);
            } else if(matrix[mid][0] > target) {
                // Target must be in a row above
                hi = mid - 1;
            } else {
                // Target must be in a row below
                lo = mid + 1;
            }
        }
        return false;  // Target not found in any row
    }
};
