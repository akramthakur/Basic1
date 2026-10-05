# Bulls and Cows - Solution

## Problem Statement
You are playing the Bulls and Cows game with a friend. You write down a secret number and ask your friend to guess it.

- **Bulls**: Digits in the correct position
- **Cows**: Digits that are in the secret but in the wrong position

Return the hint in the format "xAyB" where x is bulls and y is cows.

## Step-by-Step Logic

### Two-Pass Approach:
1. **First Pass**: Count bulls and build frequency map of non-bull secret digits
2. **Second Pass**: Count cows using the frequency map for non-bull guess digits

## Complexity Analysis

### Time Complexity: **O(n)**
- First pass: O(n) to count bulls and build frequency map
- Second pass: O(n) to count cows
- Total: O(2n) = O(n)

### Space Complexity: **O(1)**
- Hash map stores at most 10 digits (0-9)
- Constant extra space

## Final Code with Comments

```cpp
class Solution {
public:
    string getHint(string secret, string guess) {
        unordered_map<char, int> k;  // Frequency map for non-bull secret digits
        int cor = 0;  // Bulls count (correct position)
        
        // First pass: count bulls and build frequency map
        for(int i = 0; i < secret.size(); i++) {
            if(guess[i] == secret[i]) {
                cor++;  // Bull found
            } else {
                k[secret[i]]++;  // Add to frequency map for non-bull digits
            }
        }
        
        int g = 0;  // Cows count (wrong position)
        // Second pass: count cows
        for(int i = 0; i < guess.size(); i++) {
            // Check if it's a non-bull digit that exists in secret
            if(guess[i] != secret[i] && k[guess[i]] > 0) {
                g++;           // Cow found
                k[guess[i]]--; // Use up one occurrence
            }
        }
       
        // Format result string
        string res = to_string(cor) + "A" + to_string(g) + "B";
        return res;
    }
};
