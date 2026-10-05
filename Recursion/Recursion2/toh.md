# Tower of Hanoi - Solution Analysis

## Problem Statement
Solve the Tower of Hanoi problem and return the minimum number of moves required to move n disks from the first rod to the third rod.

## Issues in Current Code

### Problems Identified:
1. **Fixed Rod Numbers**: Using hardcoded 1,2,3 instead of parameters
2. **Incorrect Recursive Calls**: Not using the function parameters properly
3. **Step Counting**: Global variable approach is incorrect
4. **Missing Move Logic**: No actual disk movement simulation

## Corrected Solution

```cpp
class Solution {
public:
    // Function to solve Tower of Hanoi and return move count
    long long towerOfHanoi(int n, int from, int to, int aux) {
        if (n == 0){
            return 0;
        }
        
        // Move n-1 disks from 'from' to 'aux' using 'to' as auxiliary
        long long moves1 = towerOfHanoi(n - 1, from, aux, to);
        
        // Move the nth disk from 'from' to 'to' (count this move)
        long long currentMove = 1;
        
        // Move n-1 disks from 'aux' to 'to' using 'from' as auxiliary
        long long moves2 = towerOfHanoi(n - 1, aux, to, from);
        
        return moves1 + currentMove + moves2;
    }
};
