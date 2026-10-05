# Minimum Operations to Convert Strings - Solution

## Problem Statement
Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`. You have the following two operations permitted on a word:
- Insert a character
- Delete a character

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **State Definition**: `dp[i][j]` = minimum operations to convert first `i` characters of `word1` to first `j` characters of `word2`
2. **Base Cases**:
   - Converting to empty string: delete all characters (`dp[i][0] = i`)
   - Converting from empty string: insert all characters (`dp[0][j] = j`)
3. **Recurrence Relation**:
   - If characters match: `dp[i][j] = dp[i-1][j-1]` (no operation needed)
   - If characters differ: `min(delete, insert) + 1`

## Algorithm Details

### Operations Available:
- **Delete**: `dp[i-1][j] + 1` (remove char from word1)
- **Insert**: `dp[i][j-1] + 1` (add char to word1)

### Key Difference from Edit Distance:
- **No Replace Operation**: Only insert and delete allowed
- **Equivalent to**: Finding length of both strings and subtracting twice the LCS length

### Mathematical Insight:
Where `m` and `n` are lengths of word1 and word2 respectively.

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Fill DP table with (m+1) × (n+1) cells
- Constant time operations per cell

### Space Complexity: **O(m × n)**
- DP table of size (m+1) × (n+1)
- Can be optimized to O(min(m, n))

## Final Code with Comments

```cpp
class Solution {
public:
    int minOperations(string &word1, string &word2) {
        int m = word1.length();
        int n = word2.length();
        
        // DP table: dp[i][j] = min operations to convert word1[0..i-1] to word2[0..j-1]
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, -1));
        
        // Base case 1: Convert word1 to empty string (delete all characters)
        for(int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        
        // Base case 2: Convert empty string to word2 (insert all characters)
        for(int i = 0; i <= n; i++) {
            dp[0][i] = i;
        }
        
        // Fill DP table
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                if(word1[i - 1] == word2[j - 1]) {
                    // Characters match: no operation needed
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    // Characters differ: take minimum of delete or insert
                    dp[i][j] = min(dp[i - 1][j],  // Delete from word1
                                  dp[i][j - 1])   // Insert into word1
                              + 1;                // Cost of operation
                }
            }
        }
        
        return dp[m][n];
    }
};
