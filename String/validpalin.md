# Valid Palindrome - Solution

## Problem Statement
Given a string, determine if it is a palindrome considering only alphanumeric characters and ignoring cases.

## Step-by-Step Logic

1. **Filter Alphanumeric Characters**:
   - Create new string with only letters and numbers
   - Convert all characters to lowercase for case-insensitive comparison

2. **Two Pointer Palindrome Check**:
   - Compare characters from start and end moving towards center
   - Return false if any mismatch found
   - Return true if all characters match

## Complexity Analysis

### Time Complexity: **O(n)**
- One pass to filter alphanumeric characters: O(n)
- One pass to check palindrome: O(n/2) = O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(n)**
- Additional string `k` to store filtered characters: O(n)
- In worst case, all characters are alphanumeric

## Final Code with Comments

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        string k;  // Filtered string with only alphanumeric chars
        
        // Filter alphanumeric characters and convert to lowercase
        for(int i = 0; i < s.length(); i++){
            if((s[i] >= 'a' && s[i] <= 'z') || 
               (s[i] >= 'A' && s[i] <= 'Z') || 
               (s[i] >= '0' && s[i] <= '9')){
                k += tolower(s[i]);  // Convert to lowercase
            }
        }
        
        int n = k.size();
        // Check if filtered string is palindrome
        for(int i = 0; i < n/2; i++){
            // Compare characters from start and end
            if(k[i] != k[n - i - 1]){
                return false;  // Not a palindrome
            }
        }
        return true;  // String is palindrome
    }
};
