# Longest Increasing Subsequence - Solution

## Problem Statement
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

## Step-by-Step Logic

### Creative Approach using LCS:
1. **Key Insight**: LIS can be found by taking LCS between:
   - Original array
   - Sorted unique elements from original array
2. **Why This Works**: The sorted unique array represents all possible increasing sequences
3. **LCS Connection**: The common subsequence between original and sorted array gives the LIS

### Algorithm Steps:
1. **Remove Duplicates**: Use set to get unique elements
2. **Sort Elements**: Create sorted version of unique elements
3. **Apply LCS**: Find longest common subsequence between original and sorted array

## Complexity Analysis

### Time Complexity: **O(n²)**
- Set operations: O(n log n)
- LCS computation: O(n × n) = O(n²)
- Dominated by LCS: **O(n²)**

### Space Complexity: **O(n²)**
- DP table for LCS: O(n × n)
- Additional arrays: O(n)
- Total: **O(n²)**

## Final Code with Comments

```cpp
class Solution {
public:
    int longestCommonSubsequence(vector<int>& text1, vector<int>& text2) {
        int m = text1.size();
        int n = text2.size();
        
        // Base case: empty strings have LCS 0
        if(m == 0 || n == 0) {
            return 0;
        }
        
        // DP table: dp[i][j] = LCS of first i chars of text1 and first j chars of text2
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        
        // Fill DP table
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                if(text1[i - 1] == text2[j - 1]) {
                    // Characters match: extend previous LCS
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    // Characters don't match: take max of skipping one character
                    dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }
        return dp[m][n];
    }
    
    int lengthOfLIS(vector<int>& nums) {
        // Store original array
        vector<int> k = nums;
        
        // Remove duplicates using set (automatically sorts)
        set<int> d;
        for(int i = 0; i < nums.size(); i++) {   
            d.insert(nums[i]);
        }
        
        // Convert set to vector (now sorted unique elements)
        vector<int> compa(d.begin(), d.end());
        
        // LIS = LCS between original array and sorted unique elements
        return longestCommonSubsequence(k, compa);
    }
};
