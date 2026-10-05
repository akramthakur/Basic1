# Sudoku Solver - Solution

## Problem Statement
Given a 9×9 partially filled Sudoku board, solve the puzzle by filling the empty cells following Sudoku rules.

## Step-by-Step Logic

### Backtracking Approach:
1. **Empty Cell Identification**: Find next empty cell (marked with '.')
2. **Constraint Checking**: For each digit 1-9, verify:
   - Not present in current row
   - Not present in current column  
   - Not present in current 3×3 sub-box
3. **Recursive Exploration**: Place valid digit and recursively solve remaining board
4. **Backtracking**: If path leads to dead end, undo choice and try next digit

## Key Functions

### `checker(board, row, col, c)`
- **Purpose**: Validate if digit `c` can be placed at `(row, col)`
- **Checks**:
  - Entire row for duplicate
  - Entire column for duplicate
  - 3×3 sub-box using formula: `board[3*(row/3) + i/3][3*(col/3) + i%3]`

### `helper(board, row, col)`
- **Base Case**: Reached end of board (`row == 8 && col == 9`)
- **Row Transition**: Move to next row when column reaches 9
- **Skip Filled Cells**: If cell already filled, move to next cell
- **Digit Placement**: Try digits 1-9, backtrack if invalid

## Complexity Analysis

### Time Complexity: **O(9^(n×n))**
- In worst case, try all 9 possibilities for each of 81 cells
- Pruned significantly by constraint checking

### Space Complexity: **O(n×n)**
- Recursion stack depth up to 81 (number of cells)
- No additional data structures used

## Final Code with Comments

```cpp
class Solution {
public:
    // Check if digit 'c' can be placed at position (row, col)
    bool checker(vector<vector<char>>& board, int row, int col, char c) {
        for(int i = 0; i < 9; i++) {
            // Check entire row for duplicate
            if(board[row][i] == c) {
                return false;
            }
            // Check entire column for duplicate
            if(board[i][col] == c) {
                return false;
            }
            // Check 3x3 sub-box for duplicate
            if(board[3*(row/3) + i/3][3*(col/3) + i%3] == c) {
                return false;
            }
        }
        return true;
    }
    
    // Recursive helper function to solve Sudoku
    bool helper(vector<vector<char>>& board, int row, int col) {
        // Base case: successfully filled entire board
        if(row == 8 && col == 9) {
            return true;
        }
        
        // Move to next row when current row is complete
        if(col == 9) {
            row = row + 1;
            col = 0;
        }
        
        // Skip already filled cells
        if(board[row][col] != '.') {
            bool result = helper(board, row, col + 1);
            return result;
        }
        else {
            // Try all possible digits 1-9
            for(char i = '1'; i <= '9'; i++) {
                if(checker(board, row, col, i)) {
                    // Place digit and recursively solve
                    board[row][col] = i;
                    bool result = helper(board, row, col + 1);
                    
                    if(result == true) {
                        return true;
                    } else {
                        // Backtrack: remove invalid digit
                        board[row][col] = '.';
                    }
                }
            }
        }
        return false;
    }
    
    // Main function to solve Sudoku
    void solveSudoku(vector<vector<char>>& board) {
        helper(board, 0, 0);
    }
};
