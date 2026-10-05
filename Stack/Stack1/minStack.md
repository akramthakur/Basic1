# Min Stack - Solution

## Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

## Step-by-Step Logic

### Two-Stack Approach:
1. **Main Stack (`st`)**: Stores all elements in LIFO order
2. **Min Stack (`minst`)**: Stores minimum values in decreasing order

### Key Operations:
- **Push**: Add to main stack; add to min stack only if ≤ current min
- **Pop**: Remove from main stack; remove from min stack if it's the current min
- **Top**: Return top of main stack
- **getMin**: Return top of min stack (current minimum)

## Complexity Analysis

### Time Complexity: **O(1)** for all operations
- Push: O(1)
- Pop: O(1)  
- Top: O(1)
- getMin: O(1)

### Space Complexity: **O(n)**
- Worst case: Both stacks store n elements
- Average case: Min stack stores fewer elements

## Final Code with Comments

```cpp
class MinStack {
private:
    stack<int> st;      // Main stack for all elements
    stack<int> minst;   // Stack for minimum values
    
public:
    MinStack() {
        // Constructor - stacks are automatically initialized
    }
    
    void push(int val) {
        // Always push to main stack
        st.push(val);
        
        // Push to min stack only if:
        // - Min stack is empty (first element)
        // - Value is <= current minimum (to handle duplicates)
        if(minst.empty() || val <= minst.top()) {
            minst.push(val);
        }
    }
    
    void pop() {
        // If the element being popped is the current minimum,
        // also pop from min stack
        if(st.top() == minst.top()) {
            minst.pop();
        }
        // Always pop from main stack
        st.pop();
    }
    
    int top() {
        return st.top();
    }
    
    int getMin() {
        return minst.top();
    }
};
