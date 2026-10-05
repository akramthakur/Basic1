# Valid Parentheses - Solution

## Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid. The string is valid if:
1. Open brackets must be closed by the same type of brackets
2. Open brackets must be closed in the correct order
3. Every close bracket has a corresponding open bracket of the same type

## Step-by-Step Logic

### Stack-Based Validation:
1. **Process Characters**: Iterate through each character in string
2. **Push Opening Brackets**: Add `(`, `[`, `{` to stack
3. **Match Closing Brackets**: When encountering `)`, `]`, `}`:
   - Check if stack is not empty
   - Check if top of stack matches corresponding opening bracket
   - Pop if matched
4. **Invalid Cases**: Return false for mismatches or empty stack
5. **Final Check**: Stack must be empty at end (all brackets matched)

## Complexity Analysis

### Time Complexity: **O(n)**
- **O(n)** for single pass through the string
- **O(1)** stack operations per character
- **n** = length of the input string

### Space Complexity: **O(n)**
- **O(n)** for stack storage in worst case (all opening brackets)
- **O(1)** best case (all closing brackets or empty string)

## Final Code with Comments

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;

        for(int i = 0; i < s.length(); i++) {
            // Push opening brackets onto stack
            if(s[i] == '(' || s[i] == '[' || s[i] == '{') {
                st.push(s[i]);
            }
            // Check for matching closing brackets
            else if(s[i] == ')' && !st.empty() && st.top() == '(') {
                st.pop();
            }
            else if(s[i] == ']' && !st.empty() && st.top() == '[') {
                st.pop();
            }
            else if(s[i] == '}' && !st.empty() && st.top() == '{') {
                st.pop();
            }
            else {
                // Invalid case: mismatched bracket or stack empty
                return false;
            }
        }
        
        // All brackets matched if stack is empty
        if(st.empty())
            return true;
        return false;
    }
};
