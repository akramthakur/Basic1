# Count Vowels, Consonants and Whitespaces - Solution

## Problem Statement
Given a string, count and display the number of vowels, consonants, and whitespaces in the string. The solution should be case-insensitive.

## Step-by-Step Logic

### Character Counting Algorithm:
1. **Convert to Lowercase**: Make the string case-insensitive
2. **Character Classification**:
   - **Vowels**: 'a', 'e', 'i', 'o', 'u'
   - **Consonants**: All other alphabetic characters
   - **Whitespaces**: Space characters
3. **Count Each Category**: Iterate through string and classify each character
4. **Display Results**: Print counts for each category

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for converting string to lowercase
- **O(n)** for counting characters
- **n** = length of the string

### Space Complexity: **O(1)**
- **O(1)** - only using constant extra space for counters
- In-place modification of string (optional)

## Final Code with Comments

```cpp
#include<bits/stdc++.h>
using namespace std;

int solve(string str, int length) {
  int vowels = 0, consonants = 0, whitespaces = 0;
  
  // Convert given string to lowercase for case-insensitive comparison
  for (int i = 0; i < length; i++) {
    str[i] = tolower(str[i]);
  }
  
  // Iterate through each character and classify
  for (int i = 0; i < length; i++) {
    // Check if character is vowel
    if (str[i] == 'a' || str[i] == 'e' || str[i] == 'i' || str[i] == 'o' || str[i] == 'u')
      vowels++;
    // Check if character is consonant (alphabetic but not vowel)
    else if (str[i] >= 'a' && str[i] <= 'z')
      consonants++;
    // Check if character is whitespace
    else if (str[i] == ' ')
      whitespaces++;
  }

  // Display results
  cout << "Vowels: " << vowels << "\n";
  cout << "Consonants: " << consonants << "\n";
  cout << "White Spaces: " << whitespaces << "\n";
  
  return 0;
}

int main() {
  string str = "Hello World! Programming is Fun";
  int length = str.length();
  solve(str, length);
  return 0;
}
