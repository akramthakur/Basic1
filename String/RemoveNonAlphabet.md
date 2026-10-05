# Remove Non-Alphabet Characters - Solution

## Problem Statement
Given a string, remove all non-alphabet characters (anything that is not 'a'-'z' or 'A'-'Z') and return the resulting string containing only alphabetic characters.

## Step-by-Step Logic

### Character Filtering Algorithm:
1. **Initialize Result**: Create empty result string
2. **Iterate Through String**: Check each character
3. **Alphabet Check**: Verify if character is between 'a'-'z' or 'A'-'Z'
4. **Append Valid Characters**: Add alphabet characters to result
5. **Return Filtered String**: String containing only alphabets

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for iterating through each character once
- **O(n)** for building result string (amortized)
- **n** = length of the input string

### Space Complexity: **O(n)**
- **O(n)** for the result string storage
- **O(1)** additional space for variables

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to remove non-alphabet characters
    string removeNonAlphabets(string s) {
        string result = "";
        
        // Iterate through each character in the string
        for (char c : s) {
            // Check if character is alphabet (lowercase or uppercase)
            if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) {
                result += c;  // Append alphabet characters to result
            }
        }
        return result;
    }
};

// Driver code to test the function
int main() {
    Solution sol;
    
    string test1 = "Hello123 World! @2024";
    string test2 = "Prog$#%ramming123";
    string test3 = "A1b2C3d4";
    
    cout << "Original: \"" << test1 << "\"" << endl;
    cout << "Filtered: \"" << sol.removeNonAlphabets(test1) << "\"" << endl << endl;
    
    cout << "Original: \"" << test2 << "\"" << endl;
    cout << "Filtered: \"" << sol.removeNonAlphabets(test2) << "\"" << endl << endl;
    
    cout << "Original: \"" << test3 << "\"" << endl;
    cout << "Filtered: \"" << sol.removeNonAlphabets(test3) << "\"" << endl;
    
    return 0;
}
