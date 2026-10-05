# Priority Queue Operations - Solution

## Problem Statement
Implement three operations for a Priority Queue:
1. **insert()**: Insert an element into the priority queue
2. **find()**: Check if an element exists in the priority queue
3. **delete()**: Remove and return the maximum element from the priority queue

## Step-by-Step Logic

### Priority Queue Properties:
- **Default Behavior**: Max-heap (largest element has highest priority)
- **Insertion**: O(log n) time complexity
- **Search**: O(n) time complexity (linear scan)
- **Deletion**: O(log n) time complexity

## Complexity Analysis

### Time Complexity:
- **insert()**: O(log n) - heap insertion
- **find()**: O(n) - linear search through heap
- **delete()**: O(log n) - heap extraction

### Space Complexity: **O(1)**
- All operations use constant extra space
- Modifies the existing priority queue

## Final Code with Comments

```java
// Helper class Geeks to implement
// insert() and findFrequency()
class Geeks {

    // Function to insert element into the queue
    static void insert(PriorityQueue<Integer> q, int k) {
        // Your code here
        q.add(k);
        // Just insert k in q and don't return anything
    }

    // Function to find an element k
    static boolean find(PriorityQueue<Integer> q, int k) {
        // Your code here
        return q.contains(k);
        // If k is in q return true else return false
    }

    // Function to delete the max element from queue
    static int delete(PriorityQueue<Integer> q) {
        // Your code here
        return q.poll();
        // Delete the max element from q. The priority queue property might be useful
        // here
    }
}
