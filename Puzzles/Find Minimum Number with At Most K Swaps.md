# Find Minimum Number with At Most K Swaps - Backtracking Solution

## Problem Statement
Given a string representing a number and an integer `k`, find the minimum number that can be formed by performing at most `k` swap operations on its digits.

## Step-by-Step Logic

### Backtracking Approach:
1. **Initialization**: Start with original number as current minimum
2. **Swap Exploration**: Try all possible digit swaps
3. **Minimum Tracking**: Update global minimum when smaller number found
4. **Swap Counting**: Use remaining swaps recursively
5. **Backtracking**: Restore original state after recursive call

## Algorithm Details

### Key Operations:
- **Global Minimum**: Maintain best result found so far
- **Swap Strategy**: Only swap when `s[i] > s[j]` (greedy improvement)
- **Depth Control**: Stop when `k` swaps exhausted
- **State Restoration**: Backtrack to explore other swap sequences

### Optimization Insight:
- **Pruning**: Only consider swaps that potentially decrease the number
- **Early Comparison**: Check against minimum after each swap
- **Systematic Exploration**: Try all swap combinations within k limit

## Complexity Analysis

### Time Complexity: **O((n²)^k)**
- **Branching Factor**: O(n²) swaps at each level
- **Depth**: k levels of recursion
- **Worst Case**: Exponential in k

### Space Complexity: **O(n + k)**
- **Recursion Stack**: O(k) depth
- **String Storage**: O(n) for number representation
- **Auxiliary**: O(1) for swaps

## Code with Detailed Comments

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

// Find the minimum number formed by doing at-most `k` swap operations
void findMin(string s, int k, string &min_so_far)
{
    // Compare current number with minimum found so far
    if (min_so_far.compare(s) > 0) {
        min_so_far = s;
    }
 
    // Base case: no swaps left
    if (k < 1) {
        return;
    }
 
    int n = s.length();
 
    // Try all possible digit pairs for swapping
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            // Only swap if it can potentially create a smaller number
            if (s[i] > s[j])
            {
                // Swap digits at positions i and j
                swap(s[i], s[j]);
 
                // Recur with one less swap remaining
                findMin(s, k - 1, min_so_far);
 
                // Backtrack: restore original string
                swap(s[i], s[j]);
            }
        }
    }
}
 
// Wrapper function to initialize the process
string findMinimum(string s, int k)
{
    string min = s;  // Start with original number
    findMin(s, k, min);
    return min;
}
 
int main()
{
    string s = "934651";
    int k = 2;
 
    string min = findMinimum(s, k);
 
    cout << "The minimum number formed by doing at-most " << k
         << " swaps is " << min;
 
    return 0;
}
