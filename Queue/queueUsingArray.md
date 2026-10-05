# Queue Implementation using Vector - Solution

## Problem Statement
Implement a queue data structure using a vector with fixed maximum size, supporting basic queue operations.

## Step-by-Step Logic

### Vector-based Queue:
1. **Storage**: Use vector to store elements in FIFO order
2. **Front**: First element (index 0)
3. **Rear**: Last element (index size-1)
4. **Operations**: Enqueue at rear, dequeue from front

## Complexity Analysis

### Time Complexity:
- **enqueue()**: O(1) amortized (vector push_back)
- **dequeue()**: **O(n)** (vector erase from beginning)
- **isEmpty()**: O(1)
- **isFull()**: O(1)
- **getFront()**: O(1)
- **getRear()**: O(1)

### Space Complexity: **O(n)**
- Vector storage for n elements
- Additional variables for size tracking

## Final Code with Comments

```cpp
class myQueue {
    vector<int> arr;
    int size = 0;
    int maxsize;
    
public:
    myQueue(int n) {
        // Initialize with maximum size
        maxsize = n;
    }

    bool isEmpty() {
        // Check if queue has no elements
        return arr.empty();
    }

    bool isFull() {
        // Check if queue reached maximum capacity
        return (arr.size() == maxsize);
    }

    void enqueue(int x) {
        // Add element at rear (end of vector)
        if(arr.size() == maxsize) {
            return; // Queue full
        }
        arr.push_back(x);
        size++;
    }

    void dequeue() {
        // Remove element from front (beginning of vector)
        if(arr.empty()) {
            return; // Queue empty
        }
        arr.erase(arr.begin()); // O(n) operation
        size--;
    }

    int getFront() {
        // Get front element (first in queue)
        if(arr.empty()) {
            return -1;
        }
        return arr[0];
    }

    int getRear() {
        // Get rear element (last in queue)
        if(arr.empty()) {
            return -1;
        }
        return arr.back(); // More efficient than *(arr.end()-1)
    }
};
