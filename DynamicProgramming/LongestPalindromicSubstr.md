# Longest Palindromic Substring - Solution

## Problem Statement
Given a string `s`, return the longest palindromic substring in `s`.

A substring is a contiguous sequence of characters within the string.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to identify palindromic substrings
2. **State Definition**: `dp[j][i]` = whether substring `s[j..i]` is a palindrome
3. **Recurrence Relation**:
   - Base case: Single characters are always palindromes (`dp[i][i] = true`)
   - Two characters: `s[j] == s[i]` 
   - Longer substrings: `s[j] == s[i] && dp[j+1][i-1]`
4. **Track Longest**: Keep track of the longest palindrome found

### Key Insight:
- A substring is palindrome if:
  - First and last characters match
  - The inner substring (excluding first and last) is also palindrome
- Fill DP table by checking all possible substrings

## Complexity Analysis

### Time Complexity: **O(n²)**
- Nested loops: O(n²) substrings to check
- Constant time palindrome checks using DP

### Space Complexity: **O(n²)**
- DP table of size n × n
- Can be optimized to O(1) with center expansion

## Final Code with Comments

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.length();
        if (n == 0) return "";
        
        // DP table: dp[j][i] = is substring s[j..i] palindrome?
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        
        int maxLen = 1;  // Single character is always palindrome
        int start = 0, end = 0;
        
        // Every single character is a palindrome
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
            
            // Check all substrings ending at i
            for (int j = 0; j < i; j++) {
                // Check if s[j..i] is palindrome
                if (s[j] == s[i] && (i - j <= 2 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    
                    // Update longest palindrome found
                    if (i - j + 1 > maxLen) {
                        maxLen = i - j + 1;
                        start = j;
                        end = i;
                    }
                }
            }
        }
        
        return s.substr(start, end - start + 1);
    }
};
