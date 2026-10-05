# Wildcard Matching - Solution

## Problem Statement
Given an input string `s` and a pattern `p`, implement wildcard pattern matching with support for:
- `'?'` - Matches any single character
- `'*'` - Matches any sequence of characters (including empty sequence)

The matching should cover the **entire** input string.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to build matching solution
2. **State Definition**: `dp[i][j]` = whether first `i` chars of `s` match first `j` chars of `p`
3. **Recurrence Relation**:
   - If `p[j-1] == '*'`: `dp[i][j] = dp[i-1][j] (use * for current char) OR dp[i][j-1] (use * as empty)`
   - Else: `dp[i][j] = (chars match OR p[j-1]=='?') AND dp[i-1][j-1]`

### Key Insight:
- `'*'` can match:
  - Empty sequence: ignore `*` (`dp[i][j-1]`)
  - One or more characters: use `*` to match current char and continue using same `*` (`dp[i-1][j]`)
- `'?'` matches exactly one character

## Complexity Analysis

### Time Complexity: **O(m × n)**
- Fill DP table of size (m+1) × (n+1)
- m = length of s, n = length of p

### Space Complexity: **O(m × n)**
- DP table of size (m+1) × (n+1)
- Can be optimized to O(n)

## Final Code with Comments

```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        
        // DP table: dp[i][j] = does s[0..i-1] match p[0..j-1]?
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        
        // Base case: empty string matches empty pattern
        dp[0][0] = true;
        
        // Handle patterns starting with '*' (they can match empty string)
        for (int j = 0; j < n && p[j] == '*'; j++) {
            dp[0][j + 1] = true;
        }
        
        // Fill DP table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p[j - 1] == '*') {
                    // '*' can match:
                    // 1. Empty sequence: dp[i][j-1] (ignore '*')
                    // 2. One or more chars: dp[i-1][j] (use '*' for current char)
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                } else {
                    // Current characters match or pattern has '?'
                    // AND previous characters also match
                    dp[i][j] = (s[i - 1] == p[j - 1] || p[j - 1] == '?') 
                             && dp[i - 1][j - 1];
                }
            }
        }
        
        return dp[m][n];
    }
};
