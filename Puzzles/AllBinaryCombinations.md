# Wildcard Pattern Combinations - Solution

## Problem Statement
Given a string containing wildcard characters '?', generate all possible binary strings by replacing each '?' with either '0' or '1'.

## Step-by-Step Logic

### Backtracking Approach:
1. **Base Case**: When end of string is reached (`\0`), print the current pattern
2. **Wildcard Handling**: For each '?' encountered:
   - Replace with '0', recurse for remaining string
   - Replace with '1', recurse for remaining string
   - Backtrack to restore '?' for other combinations
3. **Fixed Character Handling**: If character is '0' or '1', simply move to next position

## Algorithm Details

### Recursive Function:
- **Parameters**: 
  - `pattern[]`: Character array (passed by reference)
  - `i`: Current index being processed
- **Termination**: When `pattern[i] == '\0'` (end of string)
- **Wildcard Processing**: Try both '0' and '1', then backtrack
- **Fixed Character**: Skip to next position without modification

### Backtracking:
- Essential because array is passed by reference
- Restores '?' after recursive calls to maintain original state

## Complexity Analysis

### Time Complexity: **O(n × 2^k)**
- `n` = length of pattern
- `k` = number of '?' characters
- Each '?' doubles the number of combinations
- Printing each combination takes O(n) time

### Space Complexity: **O(n)**
- Recursion stack depth: O(n)
- No additional data structures
- In-place modification of input array

## Code with Detailed Comments

```c
#include <stdio.h>

// Find all binary strings that can be formed from a given wildcard pattern
void printAllCombinations(char pattern[], int i)
{
    // Base case: reached end of string
    if (pattern[i] == '\0')
    {
        printf("%s\n", pattern);
        return;
    }
 
    // If the current character is '?'
    if (pattern[i] == '?')
    {
        // Try both possibilities: 0 and 1
        for (int k = 0; k < 2; k++)
        {
            // Replace '?' with current binary digit
            pattern[i] = k + '0';  // Convert 0/1 to '0'/'1'
 
            // Recur for the remaining pattern
            printAllCombinations(pattern, i + 1);
 
            // Backtrack: restore '?' for other combinations
            // Essential since array is passed by reference
            pattern[i] = '?';
        }
        return;
    }
 
    // If the current character is 0 or 1, ignore it and
    // recur for the remaining pattern
    printAllCombinations(pattern, i + 1);
}
 
int main()
{
    char pattern[] = "1?11?00?1?";
 
    printAllCombinations(pattern, 0);
 
    return 0;
}
