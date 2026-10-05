# Print Numbers from 1 to N - Solution

## Problem Statement
Print all numbers from 1 to N in increasing order using recursion.

## Step-by-Step Logic

1. **Recursive Approach**:
   - Start from 1 and increment until reaching N
   - Print current number before making recursive call
   - Stop when current number equals N

2. **Base Case**:
   - When current number `i` equals target `n`
   - Print the number and return

3. **Recursive Case**:
   - Print current number
   - Call function with next number (i+1)

## Complexity Analysis

### Time Complexity: **O(n)**
- n recursive calls for numbers 1 to n
- Each call performs constant time operations

### Space Complexity: **O(n)**
- Recursion stack depth equals n
- Each recursive call uses stack space
- For large n, this could cause stack overflow

## Final Code with Comments

```cpp
class Solution {
public:
    void rec(int n, int i) {
        // Base case: reached the target number n
        if(i == n) {
            cout << i << " ";  // Print the final number
            return;
        }
        // Print current number
        cout << i << " ";
        // Recursive call with next number
        rec(n, i + 1);
    }
    
    void printTillN(int n) {
        // Start recursion from number 1
        rec(n, 1);
    }
};
