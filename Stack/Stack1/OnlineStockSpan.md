# Online Stock Span - Solution

## Problem Statement
Design an algorithm that collects daily price quotes and returns the span of a stock's price for the current day. The span is defined as the maximum number of consecutive days (including current day) for which the stock price was less than or equal to the current price.

## Step-by-Step Logic

### Monotonic Stack Approach:
1. **Stack Storage**: Store pairs of `(price, span)` where span is consecutive days ≤ price
2. **Span Calculation**: 
   - Start with span = 1 (current day)
   - While stack top price ≤ current price: add its span to current span
   - This accumulates all previous consecutive days with prices ≤ current price
3. **Push Result**: Push `(current_price, calculated_span)` to stack

## Complexity Analysis

### Time Complexity: **O(1) amortized per operation**
- Each price pushed and popped at most once
- Amortized O(1) per `next()` call

### Space Complexity: **O(n)**
- Stack stores up to n elements in worst case (decreasing prices)
- In average case, stores fewer elements

## Final Code with Comments

```cpp
class StockSpanner {
    stack<pair<int, int>> st;  // pair<price, span>
public:
    StockSpanner() {
        // Constructor - stack automatically initialized
    }
    
    int next(int price) {
        int span = 1;  // Current day counts as 1
        
        // Accumulate spans of all previous days with price <= current price
        while(!st.empty() && st.top().first <= price) {
            span += st.top().second;  // Add the span of lower prices
            st.pop();  // Remove as they're now part of current span
        }
        
        // Push current price with its calculated span
        st.push({price, span});
        return span;
    }
};
