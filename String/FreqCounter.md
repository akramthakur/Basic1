# Character Frequency Counter - Solution

## Problem Statement
Given a string, count the frequency of each character and display the results in sorted order. The output should show each character followed by its frequency count.

## Step-by-Step Logic

### Frequency Counting Algorithm:
1. **Sort the String**: Arrange characters in alphabetical order
2. **Initialize Tracking**: Start with first character and count = 1
3. **Iterate Through String**: Compare current character with previous
4. **Count Consecutive Characters**: Increment count for same characters
5. **Output Frequency**: When character changes, output previous character and count
6. **Handle Last Character**: Output the final character count after loop

## Complexity Analysis

### Time Complexity: **O(n log n)**
- **O(n log n)** for sorting the string
- **O(n)** for the single pass through sorted string
- **n** = length of the input string

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for variables
- **O(n)** for sorting (depends on algorithm, but usually O(log n) for quicksort)

## Final Code with Comments

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

void Printfrequency(string str)
{
  // Sort the string to group identical characters together
  sort(str.begin(), str.end());
  
  // Initialize with first character
  char ch = str[0];
  int count = 1;
  
  // Iterate through the sorted string starting from second character
  for (int i = 1; i < str.length(); i++)
  {
    // If current character matches previous, increment count
    if (str[i] == ch)
      count++;
    else
    {
      // Character changed, output previous character and its count
      cout << ch << count << " ";
      count = 1;        // Reset count for new character
      ch = str[i];      // Update to new character
    }
  }
  
  // Output the last character and its count
  cout << ch << count << " ";
}

int main()
{
  string str = "shivam";
  cout << "Input: " << str << endl;
  cout << "Frequency: ";
  Printfrequency(str);
  return 0;
}
