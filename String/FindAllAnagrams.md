# Find All Anagrams in a String - Solution

## Problem Statement
Given two strings `s` and `p`, return an array of all the start indices of `p`'s anagrams in `s`.

## Step-by-Step Logic

### Algorithm:
1. **Frequency Map**: Create a frequency map of characters in string `p`
2. **Sliding Window**: Maintain a window of size `p.length()` in string `s`
3. **Counter Tracking**: Use a counter to track how many characters have matched their required frequency
4. **Window Validation**: When counter reaches 0, we found an anagram

### Key Operations:
- **Expand Window**: Move right pointer, decrement frequency in map
- **Shrink Window**: Move left pointer, increment frequency in map
- **Counter Logic**: 
  - Decrement when character frequency reaches 0
  - Increment when character frequency becomes positive again

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through string `s`
- Each character processed at most twice

### Space Complexity: **O(1)**
- Fixed size map (26 characters for lowercase English letters)
- Output space not counted

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> res;
        unordered_map<char, int> map;
        
        // Create frequency map for pattern string p
        for(int i = 0; i < p.length(); i++)
            map[p[i]]++;
        
        int cnt = map.size(); // Number of distinct characters to match
        int k = p.length();   // Window size
        int i = 0, j = 0;    // Left and right pointers
        
        while(j < s.length()) {
            // Process current character at j
            if(map.find(s[j]) != map.end()) {
                map[s[j]]--;
                if(map[s[j]] == 0) {
                    cnt--; // One character requirement satisfied
                }
            }
            
            // Expand window if size less than k
            if(j - i + 1 < k) {
                j++;
            }
            // Window size equals k
            else if(j - i + 1 == k) {
                // Check if all character requirements are satisfied
                if(cnt == 0) {
                    res.push_back(i);
                }
                
                // Remove character at i from current window
                if(map.find(s[i]) != map.end()) {
                    map[s[i]]++;
                    if(map[s[i]] == 1) {
                        cnt++; // One character requirement no longer satisfied
                    }
                }
                
                // Move window forward
                i++;
                j++;
            }
        }
        
        return res;
    }
};
