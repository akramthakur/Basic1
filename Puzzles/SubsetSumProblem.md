# Subset Sum Problem - Solution

## Problem Statement
Given an array of non-negative integers and a target sum, determine if there exists a subset of the array that adds up to exactly the target sum.

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **State Definition**: `dp[i][j]` = whether sum `j` can be achieved using first `i` elements
2. **Base Cases**:
   - Sum 0 can always be achieved (empty subset)
   - With 0 elements, only sum 0 can be achieved
3. **Recurrence Relation**:
   - If current element ≤ current sum: `dp[i][j] = dp[i-1][j-arr[i-1]] OR dp[i-1][j]`
   - Else: `dp[i][j] = dp[i-1][j]`

## Complexity Analysis

### Time Complexity: **O(n × sum)**
- Fill DP table with (n+1) × (sum+1) cells
- Constant time operations per cell

### Space Complexity: **O(n × sum)**
- DP table of size (n+1) × (sum+1)
- Can be optimized to O(sum)

## Final Code with Comments

```cpp
class Solution {
public:
    bool isSubsetSum(vector<int>& arr, int sum) {
        int n = arr.size();
        // DP table: dp[i][j] = can we make sum j using first i elements?
        vector<vector<bool>> dp(n + 1, vector<bool>(sum + 1));
       
        // Initialize DP table
        for(int i = 0; i <= n; i++) {
            for(int j = 0; j <= sum; j++) {
                if(j == 0) {
                    // Sum 0 can always be achieved (empty subset)
                    dp[i][j] = true;
                }
                if(i == 0 && j > 0) {
                    // With 0 elements, only sum 0 can be achieved
                    dp[i][j] = false;
                }
            }
        }
       
        // Fill DP table
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= sum; j++) {
                if(arr[i - 1] <= j) {
                    // Either include current element or exclude it
                    dp[i][j] = dp[i - 1][j - arr[i - 1]] || dp[i - 1][j];
                } else {
                    // Current element too large, must exclude it
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        
        return dp[n][sum];
    }
};
