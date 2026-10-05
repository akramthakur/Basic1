# Number Placement Combinations - Solution

## Problem Statement
Given a number `n`, find all combinations to place numbers from 1 to `n` in a `2n` sized array such that:
- Each number `x` appears exactly twice
- The two occurrences of `x` are exactly `x+1` positions apart
- All positions in the array are filled

## Step-by-Step Logic

### Backtracking Approach:
1. **Array Initialization**: Create `2n` sized array with `-1` (empty)
2. **Number Placement**: For each number `x`, find two positions `i` and `i+x+1` that are:
   - Both empty (`-1`)
   - Within array bounds
3. **Recursive Exploration**: Place number and recurse for next number
4. **Backtracking**: Remove number if path doesn't lead to solution

## Algorithm Details

### Key Constraints:
- **Distance Rule**: Two occurrences of `x` must be `x+1` positions apart
- **Array Size**: Exactly `2n` positions for numbers 1 to `n`
- **Complete Filling**: All positions must be occupied in final solution

### Placement Logic:
- For number `x`, try all starting positions `i` from `0` to `2n-1`
- Check if both `arr[i]` and `arr[i+x+1]` are available
- Place `x` at both positions and recurse for `x+1`

## Complexity Analysis

### Time Complexity: **O((2n)! / 2^n)**
- **Branching Factor**: Up to `2n` choices for each number
- **Pruning**: Many invalid placements are skipped
- **Exponential**: Factorial complexity in worst case

### Space Complexity: **O(n)**
- **Recursion Stack**: O(n) depth
- **Array Storage**: O(2n) for the combination array
- **Total**: O(n)

## Code with Detailed Comments

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Find all combinations that satisfy the given constraints
void findAllCombinations(vector<int> &arr, int x, int n)
{
    // Base case: all numbers from 1 to n are placed
    if (x > n)
    {
        // Print the complete combination
        for (int i : arr) {
            cout << i << " ";
        }
        cout << endl;
        return;
    }

    // Try all possible positions for the first occurrence of number `x`
    for (int i = 0; i < 2 * n; i++)
    {
        // Check if current position and position `i + x + 1` are valid
        if (arr[i] == -1 &&                           // Current position is empty
            (i + x + 1) < 2 * n &&                   // Second position within bounds
            arr[i + x + 1] == -1)                    // Second position is empty
        {
            // Place number `x` at both positions
            arr[i] = x;
            arr[i + x + 1] = x;

            // Recursively place the next number (x + 1)
            findAllCombinations(arr, x + 1, n);

            // Backtrack: remove `x` from both positions
            arr[i] = -1;
            arr[i + x + 1] = -1;
        }
    }
}

int main()
{
    // Given number
    int n = 7;

    // Create array of size 2n, all positions initialized to -1 (empty)
    vector<int> arr(2 * n, -1);

    // Start placing numbers from 1
    int x = 1;
    findAllCombinations(arr, x, n);

    return 0;
}
