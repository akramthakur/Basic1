# Evaluate Postfix Expression - Solution

## Problem Statement
Evaluate a postfix (Reverse Polish Notation) expression given as a vector of strings. The expression contains numbers and operators (+, -, *, /, ^).

## Step-by-Step Logic

1. **Stack Initialization**: Use stack to store operands
2. **Token Processing**:
   - If token is a number (including negative numbers): push to stack
   - If token is operator: pop two operands, apply operation, push result
3. **Special Handling**:
   - Negative numbers: Check if first character is '-' and string length > 1
   - Integer division: Use custom divide function for C++ truncation behavior
   - Operator precedence: Not needed in postfix evaluation

## Complexity Analysis

### Time Complexity: **O(n)**
- Process each token exactly once: O(n)
- Stack operations (push/pop): O(1) each
- Total: O(n)

### Space Complexity: **O(n)**
- Stack stores up to n/2 operands in worst case
- In balanced expression: O(n) space

## Final Code with Comments

```cpp
class Solution {
public:
    // Custom division to handle C++ integer division truncation
    int divide(int a, int b) {
        // Handle negative division with remainder
        if (a * b < 0 && a % b != 0) return a / b - 1;
        return a / b;
    }

    int evaluatePostfix(vector<string>& s) {
        stack<int> st;
        
        for(int i = 0; i < s.size(); i++) {
            // Check if token is a number (positive or negative)
            if(isdigit(s[i][0]) || (s[i][0] == '-' && s[i].size() > 1)) {
                st.push(stoi(s[i]));
            } else {
                // Token is operator - pop two operands
                int second = st.top();
                st.pop();
                int first = st.top();
                st.pop();
                int res;
                
                // Apply the operation
                if(s[i] == "+") {
                    res = first + second;
                } else if(s[i] == "-") {
                    res = first - second;
                } else if(s[i] == "*") {
                    res = first * second;
                } else if(s[i] == "/") {
                    res = divide(first, second);
                } else if(s[i] == "^") {
                    res = (int)pow(first, second);
                }
                st.push(res);
            }
        }
        return st.top();
    }
};
