# Count Words in String - Solution

## Problem Statement
Given a string, count the number of words in it. Words are separated by spaces.

## Step-by-Step Logic

### Algorithm:
1. **Initialize Counter**: Start with spaces counter at 0
2. **Iterate Through String**: Check each character
3. **Count Spaces**: Increment counter for each space character found
4. **Calculate Words**: Number of words = number of spaces + 1
5. **Return Result**: Total word count

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the string
- **n** = length of the input string

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- No additional data structures used

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string str = "HI AMY AND JAY";
    int n = str.length();
    int spaces = 0;
    
    // Count the number of spaces in the string
    for(int i = 0; i < n; i++) {
        if(str[i] == ' ')
            spaces = spaces + 1;
    }
    
    // Number of words = number of spaces + 1
    cout << "The number of words are " << spaces + 1;
    
    return 0;
}
