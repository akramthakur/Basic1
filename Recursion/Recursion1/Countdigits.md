# Count Digits - Solution

## Problem Statement
Given a number N, count the number of digits in N that evenly divide N (i.e., digits that are divisors of N).

## Step-by-Step Logic

1. **Recursive Digit Extraction**:
   - Extract digits one by one from the number
   - Check if digit is non-zero and divides the original number evenly
   - Count valid digits that satisfy the condition

2. **Base Case**:
   - Stop recursion when all digits are processed (i <= 0)

3. **Digit Validation**:
   - Skip digit if it's zero (division by zero)
   - Check if original number is divisible by the digit

## Complexity Analysis

### Time Complexity: **O(d)**
- Where d is the number of digits in N
- Each digit is processed exactly once
- For a number with d digits, time complexity is O(d)

### Space Complexity: **O(d)**
- Recursion stack depth equals number of digits
- Each recursive call uses stack space

## Final Code with Comments

```cpp
class Solution {
public:
    // Recursive function to count divisible digits
    int rec(int n, int i) {
        // Base case: no more digits to process
        if(i <= 0) {
            return 0;
        }
        
        // Extract last digit
        int digit = (i % 10);
        
        // Check if digit is non-zero and divides n evenly
        if(digit != 0 && n % digit == 0)
            return 1 + rec(n, i / 10);  // Count this digit and process remaining
        else 
            return rec(n, i / 10);      // Skip this digit, process remaining
    }
    
    int evenlyDivides(int n) {
        // Start recursion with the number itself
        int ans = rec(n, n);
        return ans;
    }
};
