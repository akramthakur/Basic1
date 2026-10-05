# Maximum Occurring Character - Solution

## Problem Statement
Given a string, find the character that occurs the maximum number of times. If multiple characters have the same maximum frequency, return the character that appears first in alphabetical order.

## Step-by-Step Logic

### Algorithm:
1. **Sort the String**: Arrange characters in alphabetical order
2. **Initialize Tracking**: Start with first character and frequency counters
3. **Traverse Sorted String**: Compare consecutive characters
4. **Count Frequencies**: Track current character frequency and maximum frequency
5. **Update Maximum**: When character changes, check if current frequency > maximum frequency
6. **Handle Last Character**: Final check after loop completion
7. **Return Result**: Character with highest frequency (alphabetically first in case of ties)

## Complexity Analysis

### Time Complexity: **O(n log n)**
- **O(n log n)** for sorting the string
- **O(n)** for the single pass through sorted string
- **n** = length of the input string

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- **O(n)** for sorting (depends on algorithm implementation)

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to find max occurring character
    char getMaxOccurringChar(string s) {
        // Sort the string to group identical characters
        sort(s.begin(), s.end());

        // Variables to store result
        int maxFreq = 1, currFreq = 1;
        char maxChar = s[0];

        // Traverse the sorted string
        for (int i = 1; i < s.size(); i++) {
            // If same character as previous, increase count
            if (s[i] == s[i - 1]) {
                currFreq++;
            } 
            else {
                // Character changed, check if previous character has higher frequency
                if (currFreq > maxFreq) {
                    maxFreq = currFreq;
                    maxChar = s[i - 1];
                }
                // Reset count for new character
                currFreq = 1;
            }
        }

        // Final check for the last character sequence
        if (currFreq > maxFreq) {
            maxFreq = currFreq;
            maxChar = s[s.size() - 1];
        }

        // Return the character with maximum frequency
        return maxChar;
    }
};

int main() {
    // Input string
    string s = "samplestring";

    // Create object of Solution
    Solution obj;

    // Call function
    char ans = obj.getMaxOccurringChar(s);

    // Print result
    cout << "Max occurring character: " << ans << endl;
    return 0;
}
