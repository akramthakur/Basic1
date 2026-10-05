# Longest Common Subsequence - Solution

## Problem Statement
Given two strings `text1` and `text2`, return the length of their longest common subsequence (LCS).

A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to build solution
2. **State Definition**: `dp[i][j]` = LCS length of first `i` chars of text1 and first `j` chars of text2
3. **Recurrence Relation**:
   - If characters match: `dp[i][j] = 1 + dp[i-1][j-1]`
   - If characters don't match: `dp[i][j] = max(dp[i][j-1], dp[i-1][j])`
4. **Base Cases**: First row and column are 0 (empty string vs any string)

### Key Insight:
- Build solution incrementally by comparing prefixes
- When characters match, extend LCS from previous diagonal
- When characters don't match, take best of excluding one character from either string

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Fill DP table with (m+1) × (n+1) cells
- Constant time operations per cell

### Space Complexity: **O(m × n)**
- DP table of size (m+1) × (n+1)
- Can be optimized to O(min(m,n))

## Final Code with Comments

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.length();
        int n = text2.length();
        
        // Handle empty strings
        if (m == 0 || n == 0) {
            return 0;
        }
        
        // DP table: dp[i][j] = LCS of text1[0..i-1] and text2[0..j-1]
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        
        // Fill DP table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1[i - 1] == text2[j - 1]) {
                    // Characters match: extend LCS from previous diagonal
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    // Characters don't match: take maximum of excluding one character
                    dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }
        
        return dp[m][n];
    }
};
