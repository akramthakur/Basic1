# Single Number II - Solution

## Problem Statement
Given an array of integers where every element appears **three times** except for one element which appears exactly once, find that single element.

## Step-by-Step Logic

### Algorithm:
1. **Bit Counting Approach**: Track the count of 1-bits at each position modulo 3
2. **Two Variables**: Use `ones` and `twos` to represent bit counts
   - `ones`: bits that have appeared once (mod 3)
   - `twos`: bits that have appeared twice (mod 3)
3. **Bitwise Operations**: Update counts using XOR and AND operations

### Key Insight:
- We need to count occurrences of each bit position modulo 3
- The unique number will have bits that don't cancel out after counting modulo 3

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the array
- Constant time bit operations per element

### Space Complexity: **O(1)**
- Only two integer variables used

## Final Code with Comments

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones = 0;  // Tracks bits that have appeared once (mod 3)
        int twos = 0;  // Tracks bits that have appeared twice (mod 3)
        
        for(int i = 0; i < nums.size(); i++) {
            // Update 'ones': 
            // XOR with current number, but remove bits that are in 'twos'
            ones = (ones ^ nums[i]) & ~twos;
            
            // Update 'twos':
            // XOR with current number, but remove bits that are in 'ones'  
            twos = (twos ^ nums[i]) & ~ones;
        }
        
        return ones;  // The bits that remain in 'ones' is our answer
    }
};
