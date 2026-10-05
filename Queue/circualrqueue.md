# Circular Queue Implementation - Solution

## Problem Statement
Design a circular queue implementation with fixed size that supports efficient enqueue, dequeue, and access operations.

## Step-by-Step Logic

### Circular Array Approach:
1. **Storage**: Fixed-size array with circular indexing
2. **Pointers**: 
   - `front`: Points to first element
   - `rear`: Points to last element
   - Both initialized to -1 (empty queue)

3. **Circular Indexing**: Use modulo arithmetic for wrap-around
   - `next_index = (current + 1) % n`

## Complexity Analysis

### Time Complexity: **O(1)** for all operations
- **enQueue**: O(1) - direct array access
- **deQueue**: O(1) - pointer update
- **Front/Rear**: O(1) - direct access
- **isEmpty/isFull**: O(1) - condition checks

### Space Complexity: **O(n)**
- Array of size n for storage
- Constant space for pointers

## Final Code with Comments

```cpp
class MyCircularQueue {
    vector<int> queue;
    int front;
    int rear;
    int n;
    
public:
    MyCircularQueue(int k) {
        n = k;
        queue.resize(n);
        front = rear = -1;  // Empty queue indicator
    }
    
    bool enQueue(int value) {
        if(isFull()) {
            return false;  // Queue full
        }
        
        if(rear == -1) {
            // First element - initialize both pointers
            front = 0;
            rear = 0;
        } else {
            // Move rear circularly
            rear = (rear + 1) % n;
        }
        
        queue[rear] = value;
        return true;
    }
    
    bool deQueue() {
        if(isEmpty()) {
            return false;  // Queue empty
        }
        
        if(front == rear) {
            // Last element - reset to empty
            front = rear = -1;
        } else {
            // Move front circularly
            front = (front + 1) % n;
        }
        return true;
    }
    
    int Front() {
        if(isEmpty()) {
            return -1;
        }
        return queue[front];
    }
    
    int Rear() {
        if(isEmpty()) {
            return -1;
        }
        return queue[rear];
    }
    
    bool isEmpty() {
        return rear == -1;  // Both front and rear are -1 when empty
    }
    
    bool isFull() {
        return (rear + 1) % n == front;  // Next position equals front
    }
};
