# Super Egg Drop - Solution

## Problem Statement
You are given `k` identical eggs and you have access to a building with `n` floors labeled from `1` to `n`.

You need to find the **minimum number of moves** required to find the highest floor from which an egg can be dropped without breaking.

## Step-by-Step Logic

### Algorithm:
1. **Binary Search with Dynamic Programming**: Optimize the worst-case scenario
2. **State Definition**: `mem[k][n]` = minimum moves with `k` eggs and `n` floors
3. **Recurrence with Binary Search**: 
   - At each decision point, choose a floor `mid` to drop the egg
   - If egg breaks: check lower floors `(k-1, mid-1)`
   - If egg survives: check higher floors `(k, n-mid)`
   - Take maximum of both cases (worst-case) + 1 for current move
4. **Binary Search Optimization**: Instead of checking all floors, use binary search to find optimal floor

### Key Insight:
- This is an **optimization problem** where we want to minimize worst-case moves
- Traditional DP would be O(kn²), but binary search reduces to O(kn log n)
- At each state, we're finding the floor that minimizes the worst-case scenario

## Complexity Analysis

### Time Complexity: **O(k × n log n)**
- k states for eggs
- n states for floors  
- Binary search per state: O(log n)

### Space Complexity: **O(k × n)**
- DP memoization table of size k × n

## Final Code with Comments

```cpp
class Solution {
public:
    int helper(int k, int n, vector<vector<int>>& mem) {
        // Base cases
        if (n == 0 || n == 1 || k == 1) return n;
        if (mem[k][n] != -1) return mem[k][n];

        int mn = INT_MAX;
        int low = 0, high = n;
        
        // Binary search for optimal floor
        while (low <= high) {
            int mid = low + (high - low) / 2;
            
            // If egg breaks at mid, check lower floors with k-1 eggs
            int left = helper(k - 1, mid - 1, mem);
            // If egg survives at mid, check higher floors with k eggs  
            int right = helper(k, n - mid, mem);
            
            // Worst case: take maximum of both possibilities
            int temp = 1 + max(left, right);
            
            // Binary search optimization
            if (left < right) {
                low = mid + 1;  // Need to check higher floors
            } else {
                high = mid - 1; // Need to check lower floors
            }
            
            mn = min(mn, temp);  // Track minimum worst-case
        }
        
        return mem[k][n] = mn;
    }

    int superEggDrop(int k, int n) {
        // Memoization table: mem[eggs][floors]
        vector<vector<int>> mem(k + 1, vector<int>(n + 1, -1));
        return helper(k, n, mem);
    }
};
