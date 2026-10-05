# Optimal Binary Search Tree - Dynamic Programming Solution

## Problem Statement
Given a sorted array of keys and their corresponding search frequencies, construct a binary search tree that minimizes the total cost of all searches. The cost of searching a key is equal to its frequency multiplied by its depth in the tree (root depth = 1).

## Step-by-Step Logic

### Dynamic Programming Approach:
1. **Subproblem Definition**: `dp[i][j]` = minimum cost for keys from index `i` to `j`
2. **Base Cases**: 
   - Single key: cost = its frequency (depth 1)
   - Empty subtree: cost = 0
3. **Recurrence Relation**: Try each key as root, minimize sum of left subtree, right subtree, and current level cost
4. **Cost Calculation**: When making key `k` as root, all keys in range `[i,j]` move one level deeper

## Algorithm Details

### Key Insight:
- For keys `i` to `j`, if we make key `k` as root:
  - Left subtree: keys `i` to `k-1`
  - Right subtree: keys `k+1` to `j`
  - Total cost = left_cost + right_cost + sum(freq[i..j])

### Why Add Sum of Frequencies:
- When key `k` becomes root, all keys in current subtree move one level deeper
- This adds their frequencies to the total cost once for this level

## Complexity Analysis

### Time Complexity: **O(n³)**
- **Number of Subproblems**: O(n²) ranges [i,j]
- **Time per Subproblem**: O(n) to try all roots
- **Total**: O(n³)

### Space Complexity: **O(n²)**
- **DP Table**: n × n matrix
- **Recursion Stack**: O(n) in worst case

## Code with Detailed Comments

```cpp
class Solution {
public:
    int solve(int i, int j, int *keys, int *freq, vector<vector<int>>& dp) {
        // Base case: single key - cost is its frequency (depth 1)
        if (i == j) {
            return freq[i];
        }
        
        // Base case: empty subtree - cost is 0
        if (i > j) {
            return 0;
        }
        
        // Return memoized result if available
        if (dp[i][j] != -1) {
            return dp[i][j];
        }
        
        // Calculate sum of frequencies in current range [i, j]
        int cur = 0;
        for (int k = i; k <= j; k++) {
            cur += freq[k];
        }
        
        int ans = INT_MAX;
        
        // Try each key in range [i, j] as root
        for (int k = i; k <= j; k++) {
            // Cost of left subtree (keys i to k-1)
            int left = solve(i, k - 1, keys, freq, dp);
            
            // Cost of right subtree (keys k+1 to j)
            int right = solve(k + 1, j, keys, freq, dp);
            
            // Total cost = left + right + sum of all frequencies in current range
            // The sum is added because making this subtree moves all keys one level deeper
            ans = min(ans, left + right + cur);
        }
        
        return dp[i][j] = ans;
    }
    
    int optimalSearchTree(int keys[], int freq[], int n) {
        // DP table: dp[i][j] = min cost for keys from index i to j
        vector<vector<int>> dp(n, vector<int>(n, -1));
        
        return solve(0, n - 1, keys, freq, dp);
    }
};
