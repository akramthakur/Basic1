# Remove Duplicate Characters - Solution

## Problem Statement
Given a string, remove all duplicate characters and return a new string containing only the first occurrence of each character, maintaining the original order of first occurrences.

## Step-by-Step Logic

### Algorithm:
1. **Frequency Tracking**: Use an array to track seen characters (ASCII 256)
2. **Result Building**: Initialize empty result string
3. **Character Processing**: For each character in input string:
   - If character not seen before, add to result
   - Mark character as seen
4. **Return Result**: String with duplicates removed

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the string
- **O(1)** for character lookups in frequency array
- **n** = length of the input string

### Space Complexity: **O(1)**
- **O(256)** = **O(1)** for frequency array (fixed size)
- **O(n)** for result string in worst case (no duplicates)
- Considered O(1) auxiliary space

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to remove duplicate characters
string removeDuplicates(string &s)
{
    // Create an integer array to store 
    // frequency for ASCII characters (0-255)
    vector<int> ch(256, 0);

    // Create result string
    string ans = "";

    // Traverse the input string
    for (char c : s) {
      
        // Check if current character's frequency is 0
        // (meaning we haven't seen this character before)
        if (ch[c] == 0) {
          
            // Add character to result if it's the first occurrence
            ans.push_back(c);

            // Mark character as seen by incrementing frequency
            ch[c]++;
        }
    }
    return ans;
}

// Driver code
int main()
{
    string s = "shivam";
    cout << "Original: " << s << endl;
    cout << "After removing duplicates: " << removeDuplicates(s) << endl;
    return 0;
}
