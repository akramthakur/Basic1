# Longest Substring Without Repeating Characters - Solution

## Problem Statement
Given a string `s`, find the length of the longest substring without repeating characters.

## Step-by-Step Logic

### Sliding Window with Hash Map:
1. **Two Pointers**: `left` and `right` define the current window
2. **Character Tracking**: Hash map stores the most recent index of each character
3. **Window Adjustment**: When duplicate found, move `left` pointer to position after last occurrence
4. **Max Length Tracking**: Update maximum length at each step

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through the string
- Each character processed exactly once
- Hash map operations: O(1) average case

### Space Complexity: **O(min(m, n))**
- Hash map stores character indices
- m = size of character set (ASCII: 128, Unicode: more)
- In practice: O(1) for fixed character sets

## Final Code with Comments

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> index;  // Stores last index of each character
        int left = 0, maxi = 0;         // Left pointer and max length
        
        for (int right = 0; right < s.size(); ++right) {
            // If character exists in current window, update left pointer
            if (index.find(s[right]) != index.end()) {
                left = max(left, index[s[right]] + 1);
            }
            
            // Update character's last seen index
            index[s[right]] = right;
            
            // Update maximum length
            maxi = max(maxi, right - left + 1);
        }
        return maxi;
    }
};
