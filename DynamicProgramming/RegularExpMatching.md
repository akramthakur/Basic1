# Regular Expression Matching - Solution

## Problem Statement
Given an input string `s` and a pattern `p`, implement regular expression matching with support for:
- `'.'` - Matches any single character
- `'*'` - Matches zero or more of the preceding element

The matching should cover the **entire** input string.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to build matching solution
2. **State Definition**: `dp[i][j]` = whether first `i` chars of `s` match first `j` chars of `p`
3. **Recurrence Relation**:
   - If `p[j-1] == '.' OR p[j-1] == s[i-1]`: `dp[i][j] = dp[i-1][j-1]`
   - If `p[j-1] == '*'`: 
     - Zero occurrences: `dp[i][j-2]`
     - One or more occurrences: if preceding char matches, `dp[i-1][j]`

### Key Insight:
- `'*'` is the most complex case - it can match:
  - **Zero occurrences** of preceding char: ignore `char*` entirely (`dp[i][j-2]`)
  - **One or more occurrences**: if preceding char matches current char, continue using same pattern (`dp[i-1][j]`)

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
        int n = s.size(), m = p.size();
        
        // DP table: dp[i][j] = does s[0..i-1] match p[0..j-1]?
        vector<vector<bool>> dp(n + 1, vector<bool>(m + 1, false));
        
        // Base case: empty string matches empty pattern
        dp[0][0] = true;
        
        // Handle patterns like "a*", "a*b*", "a*b*c*" that can match empty string
        for (int j = 1; j <= m; j++) {
            if (p[j - 1] == '*' && dp[0][j - 2]) {
                dp[0][j] = true;
            }
        }
        
        // Fill DP table
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (p[j - 1] == '.' || p[j - 1] == s[i - 1]) {
                    // Current characters match directly or pattern has '.'
                    dp[i][j] = dp[i - 1][j - 1];
                } 
                else if (p[j - 1] == '*') {
                    // Case 1: Zero occurrences of preceding character
                    dp[i][j] = dp[i][j - 2];
                    
                    // Case 2: One or more occurrences of preceding character
                    // Check if preceding character matches current string character
                    if (p[j - 2] == '.' || p[j - 2] == s[i - 1]) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }
        
        return dp[n][m];
    }
};
