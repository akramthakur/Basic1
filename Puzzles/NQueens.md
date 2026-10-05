# N-Queens - Solution

## Problem Statement
The n-queens puzzle is the problem of placing `n` queens on an `n × n` chessboard such that no two queens attack each other. Given an integer `n`, return all distinct solutions to the n-queens puzzle.

Each solution contains distinct board configurations where `'Q'` and `'.'` indicate queen and empty space respectively.

## Step-by-Step Logic

### Algorithm:
1. **Backtracking with Pruning**: Systematically place queens row by row
2. **Conflict Detection**: Use three boolean arrays to track attacked positions
   - `rows`: Track occupied columns
   - `diag1`: Track main diagonals (row + column)
   - `diag2`: Track anti-diagonals (row - column + n)
3. **State Representation**: `board[i] = j` means queen at row `i`, column `j`

### Key Insight:
- Place one queen per row (since queens attack horizontally)
- For each row, try all columns that don't conflict with previous queens
- Use diagonal properties to quickly check conflicts:
  - Main diagonal: `row + column = constant`
  - Anti-diagonal: `row - column = constant`

## Complexity Analysis

### Time Complexity: **O(n!)**
- First row: n choices
- Second row: ~n-1 choices (pruned by constraints)
- Exponential but heavily pruned

### Space Complexity: **O(n)**
- Recursion stack: O(n)
- Boolean arrays: O(n)
- Output: O(n × solution_count) not counted

## Final Code with Comments

```cpp
class Solution {
public:
    void helper(int i, int n, vector<int>& board, vector<bool>& rows, 
                vector<bool>& diag1, vector<bool>& diag2, vector<vector<int>>& res) {
        // Base case: all queens placed successfully
        if (i > n) {
            res.push_back(board);
            return;
        }
        
        // Try placing queen in each column of current row
        for (int j = 1; j <= n; j++) {
            // Check if column and both diagonals are safe
            if (!rows[j] && !diag1[j + i] && !diag2[j - i + n]) {
                // Place queen and mark attacked positions
                rows[j] = diag1[j + i] = diag2[j - i + n] = true;
                board.push_back(j);  // Store column position for current row
                
                // Recurse for next row
                helper(i + 1, n, board, rows, diag1, diag2, res);
                
                // Backtrack: remove queen and unmark positions
                board.pop_back();
                rows[j] = diag1[j + i] = diag2[j - i + n] = false;
            }
        }
    }
    
    vector<vector<int>> nQueen(int n) {
        vector<vector<int>> res;
        vector<int> board;  // board[i] = column of queen in row i
        
        // Tracking arrays
        vector<bool> rows(n + 1, false);        // Occupied columns
        vector<bool> diag1(2 * n + 1, false);   // Main diagonals: row + col
        vector<bool> diag2(2 * n + 1, false);   // Anti-diagonals: row - col + n
        
        helper(1, n, board, rows, diag1, diag2, res);
        return res;
    }
};
