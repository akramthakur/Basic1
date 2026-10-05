# Longest Palindromic Subsequence - Solution

## Problem Statement
Given a string `s`, find the longest palindromic subsequence's length in `s`.

A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

## Step-by-Step Logic

### Algorithm:
1. **Key Insight**: The longest palindromic subsequence (LPS) of a string is the **Longest Common Subsequence (LCS)** between the string and its reverse
2. **Reverse String**: Create the reverse of the input string
3. **LCS Application**: Find LCS between original string and its reverse

### Why This Works:
- A palindrome reads the same forwards and backwards
- The LCS between a string and its reverse finds the longest sequence that appears in the same order in both directions
- This automatically gives us the longest palindromic subsequence

## Complexity Analysis

### Time Complexity: **O(n²)**
- LCS computation between two strings of length n
- Filling DP table of size (n+1) × (n+1)

### Space Complexity: **O(n²)**
- DP table for LCS computation
- Can be optimized to O(n)

## Final Code with Comments

```cpp
class Solution {
public:
    // Helper function to compute Longest Common Subsequence
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.length();
        int n = text2.length();
        
        if (m == 0 || n == 0) {
            return 0;
        }
        
        // DP table: dp[i][j] = LCS of first i chars of text1 and first j chars of text2
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1[i - 1] == text2[j - 1]) {
                    // Characters match: extend LCS
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    // Characters don't match: take maximum of two possibilities
                    dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }
        return dp[m][n];
    }

    int longestPalindromeSubseq(string s) {
        // Create reverse of the input string
        string t = s;
        reverse(t.begin(), t.end());
        
        // LPS(s) = LCS(s, reverse(s))
        return longestCommonSubsequence(s, t);
    }
};
