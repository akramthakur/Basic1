# Queue using Stacks - Solution

## Problem Statement
Implement a queue (FIFO) using only two stacks. The queue should support all standard operations: push, pop, peek, and empty.

## Step-by-Step Logic

### Two-Stack Approach:
1. **Input Stack (`inp`)**: All new elements are pushed here
2. **Output Stack (`out`)**: Elements are popped from here in FIFO order
3. **Transfer Logic**: When output stack is empty, transfer all elements from input stack (reversing order)

### Key Insight:
- Stack is LIFO (Last In First Out)
- Two stacks can simulate FIFO by reversing order twice
- **Amortized O(1)** complexity per operation

## Complexity Analysis

### Time Complexity: **Amortized O(1) per operation**
- **push(x)**: O(1) - direct push to input stack
- **pop()**: Amortized O(1) - occasional O(n) transfer
- **peek()**: Amortized O(1) - occasional O(n) transfer
- **empty()**: O(1) - check both stacks

### Space Complexity: **O(n)**
- Two stacks storing n elements total
- No additional data structures

## Final Code with Comments

```cpp
class MyQueue {
    stack<int> inp;  // Input stack - for push operations
    stack<int> out;  // Output stack - for pop/peek operations

public:
    MyQueue() {
        // Constructor - stacks automatically initialized
    }
    
    void push(int x) {
        // Always push to input stack - O(1)
        inp.push(x);
    }
    
    int pop() {
        // If output stack is empty, transfer all elements from input
        if(out.empty()) {
            while (!inp.empty()) {
                out.push(inp.top());  // Reverse order
                inp.pop();
            }
        }
        
        // Pop from output stack (front of queue)
        int val = out.top();
        out.pop();
        return val;
    }
    
    int peek() {
        // If output stack is empty, transfer all elements from input
        if(out.empty()) {
            while (!inp.empty()) {
                out.push(inp.top());  // Reverse order
                inp.pop();
            }
        }
        
        // Return front element without popping
        return out.top();
    }
    
    bool empty() {
        // Queue is empty only when both stacks are empty
        return (inp.empty() && out.empty());
    }
};
