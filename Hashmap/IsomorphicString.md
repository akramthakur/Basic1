# Isomorphic Strings - Solution

## Problem Statement
Given two strings `s` and `t`, determine if they are isomorphic. Two strings are isomorphic if the characters in `s` can be replaced to get `t`. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

## Step-by-Step Logic

### Two-Way Mapping Approach:
1. **Create two hash maps**: One for mapping s→t and another for mapping t→s
2. **Iterate through characters**: For each character pair (s[i], t[i])
3. **Check mapping consistency**:
   - If both characters are unmapped, create new mappings
   - If mappings exist, verify they match current characters
4. **Return false** if any inconsistency is found

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through both strings
- **O(1)** hash map operations per character

### Space Complexity: **O(1)**
- **O(256)** for character mappings (constant space)
- Stores at most 256 characters for ASCII

## Final Code with Comments

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        // Two maps for bidirectional mapping check
        unordered_map<char, char> map1; // s -> t mapping
        unordered_map<char, char> map2; // t -> s mapping
        
        for(int i = 0; i < s.size(); i++) {
            // If both characters are not mapped yet
            if(map1.find(s[i]) == map1.end() && map2.find(t[i]) == map2.end()) {
                map1[s[i]] = t[i];  // Create s -> t mapping
                map2[t[i]] = s[i];  // Create t -> s mapping
            } else {
                // Check if existing mappings are consistent
                if(map1[s[i]] != t[i] || map2[t[i]] != s[i]) {
                    return false;  // Mapping conflict found
                }
            }
        }
        return true;  // All mappings are consistent
    }
};
