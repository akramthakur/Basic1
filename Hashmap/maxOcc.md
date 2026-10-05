# Maximum Occurring Character - Solution

## Problem Statement
Given a string, find the maximum occurring character in the string. If multiple characters have the same maximum frequency, return the lexicographically smallest character.

## Step-by-Step Logic

### Current Approach:
1. **Sort String**: Sort the string (unnecessary step)
2. **Count Frequencies**: Use hash map to count character occurrences
3. **Find Maximum**: Iterate through map to find char with max frequency
4. **Tie-breaker**: Choose lexicographically smallest for same frequency

## Complexity Analysis

### Current Implementation:
- **Time Complexity**: O(n log n) + O(n) + O(26) = **O(n log n)**
  - Sorting: O(n log n)
  - Frequency counting: O(n)
  - Finding max: O(26) for lowercase letters
- **Space Complexity**: O(26) = O(1) for hash map

## Optimized Solution

### Single Pass with Array - O(n) time
```cpp
class Solution {
public:
    char getMaxOccuringChar(string& s) {
        int freq[26] = {0};  // For lowercase letters only
        
        // Count frequencies
        for(char c : s) {
            freq[c - 'a']++;
        }
        
        int maxFreq = 0;
        char result = 'z';  // Start with largest for tie-breaking
        
        // Find maximum frequency character (lexicographically smallest for ties)
        for(int i = 0; i < 26; i++) {
            if(freq[i] > maxFreq) {
                maxFreq = freq[i];
                result = 'a' + i;
            }
        }
        
        return result;
    }
};
