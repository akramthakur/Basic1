# Lemonade Change - Solution

## Problem Statement
At a lemonade stand, each lemonade costs $5. Customers are standing in a queue to buy from you and order one at a time. Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill. You must provide the correct change to each customer so that the net transaction is that the customer pays $5.

Return `true` if you can provide every customer with correct change, otherwise `false`.

## Step-by-Step Logic

### Algorithm:
1. **Track Bills**: Keep count of $5 and $10 bills available
2. **Greedy Change Giving**: Always use larger bills first when giving change
3. **Three Cases**:
   - $5 bill: No change needed, keep the $5
   - $10 bill: Need to give $5 change
   - $20 bill: Need to give $15 change (prefer $10 + $5 over 3 × $5)

### Key Insight:
- For $20 bills, always use a $10 + $5 if available (saves $5 bills)
- Only $5 bills can be used as change for $10 bills
- If we run out of $5 bills at any point, it's impossible to give correct change

## Complexity Analysis

### Time Complexity: **O(n)**
- Single pass through all bills
- Constant time operations per bill

### Space Complexity: **O(1)**
- Only two integer counters used

## Final Code with Comments

```cpp
class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        int five = 0, ten = 0;  // Count of $5 and $10 bills
        
        for (int i = 0; i < bills.size(); i++) {
            if (bills[i] == 5) {
                // $5 bill: no change needed
                five++;
            } 
            else if (bills[i] == 10) {
                // $10 bill: need to give $5 change
                if (five > 0) {
                    five--;
                    ten++;
                } else {
                    return false;  // Cannot give change
                }
            } 
            else {  // $20 bill
                // Prefer $10 + $5 over 3 × $5
                if (five > 0 && ten > 0) {
                    five--;
                    ten--;
                } 
                else if (five >= 3) {
                    five -= 3;
                } 
                else {
                    return false;  // Cannot give $15 change
                }
            }
        }
        return true;
    }
};
