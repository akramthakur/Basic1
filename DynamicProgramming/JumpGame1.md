# Jump Game - Solution

## Problem Statement
Given an array `nums` of non-negative integers, you are initially positioned at the first index. Each element in the array represents your maximum jump length at that position.

Determine if you can reach the last index.

## Step-by-Step Logic

### Algorithm:
1. **DFS with Memoization**: Recursively explore all possible jumps from each position
2. **State Definition**: `dp[i]` = whether we can reach the last index from position `i`
3. **Recurrence Relation**: 
   - From position `i`, try all jumps from 1 to `nums[i]`
   - If any jump leads to a position that can reach the end, return true
4. **Base Cases**:
   - If `i >= nums.size()-1`, reached/overshot the end → return true
   - If `nums[i] == 0`, cannot jump anywhere → return false

### Key Insight:
- This is a reachability problem in an implicit graph
- At each position, we can jump up to `nums[i]` steps forward
- Memoization prevents exponential time complexity

## Complexity Analysis

### Time Complexity: **O(n²)**
- In worst case, each position can jump to all subsequent positions
- With memoization, each state is computed once

### Space Complexity: **O(n)**
- DP array of size n
- Recursion stack depth: O(n) in worst case

## Final Code with Comments

```cpp
class Solution {
public:
    bool solve(vector<int>& nums, int i, vector<int>& dp) {
        // Base case: reached or overshot the last index
        if (i >= nums.size() - 1) return true;
        
        // Return cached result if available
        if (dp[i] != -1) return dp[i];
        
        // If current position has 0 jump capacity, cannot proceed
        if (nums[i] == 0) return dp[i] = false;
        
        // Try all possible jumps from current position
        for (int j = 1; j <= nums[i]; j++) {
            if (solve(nums, i + j, dp)) {
                return dp[i] = true;
            }
        }
        
        // No jump from this position leads to the end
        return dp[i] = false;
    }
    
    bool canJump(vector<int>& nums) {
        // Single element array: already at the end
        if (nums.size() == 1) return true;
        
        // DP array for memoization: -1 = uncomputed, 0 = false, 1 = true
        vector<int> dp(nums.size(), -1);
        
        return solve(nums, 0, dp);
    }
};
