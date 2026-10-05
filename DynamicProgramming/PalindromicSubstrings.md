# Palindromic Substrings - Solution

## Problem Statement
Given a string `s`, return the number of palindromic substrings in it.

A substring is a contiguous sequence of characters within the string.

## Step-by-Step Logic

### Algorithm:
1. **Dynamic Programming**: Use bottom-up approach to identify all palindromic substrings
2. **State Definition**: `dp[j][i]` = whether substring `s[j..i]` is a palindrome
3. **Recurrence Relation**:
   - Base case: Single characters are always palindromes
   - Two characters: `s[j] == s[i]`
   - Longer substrings: `s[j] == s[i] && dp[j+1][i-1]`
4. **Count All**: Increment count for every palindrome found

### Key Insight:
- A substring is palindrome if:
  - First and last characters match
  - The inner substring (excluding first and last) is also palindrome
- Count all possible palindromic substrings by checking all substrings

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
    int helper(string s) {
        int n = s.length();
        // DP table: dp[j][i] = is substring s[j..i] palindrome?
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        
        int count = 0;
        
        for (int i = 0; i < n; i++) {
            // Every single character is a palindrome
            dp[i][i] = true;
            count++;
            
            // Check all substrings ending at i
            for (int j = 0; j < i; j++) {
                // Check if s[j..i] is palindrome
                if (s[j] == s[i] && (i - j <= 2 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    count++;
                }
            }
        }
        return count;
    }
    
    int countSubstrings(string s) {
        return helper(s);
    }
};
