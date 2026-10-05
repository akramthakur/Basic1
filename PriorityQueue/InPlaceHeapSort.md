# Inplace Heap Sort - Solution

## Problem Statement
Implement heap sort algorithm that sorts an array in ascending order using in-place operations without using extra space.

## Step-by-Step Logic

### Algorithm:
1. **Build Max Heap**: Convert the array into a max heap
2. **Sort**:
   - Repeatedly swap root (max element) with last element
   - Reduce heap size and heapify the root
   - Continue until heap size becomes 1

### Key Operations:
- **Heapify**: Maintain max heap property from given index
- **Parent-Child Relations**:
  - Parent at index `i`
  - Left child at `2*i + 1`
  - Right child at `2*i + 2`

## Complexity Analysis

### Time Complexity: **O(n log n)**
- Building heap: O(n)
- Each extraction: O(log n)
- Total: O(n log n)

### Space Complexity: **O(1)**
- Completely in-place, no extra space used

## Final Code with Comments

```cpp
class Solution {
public:
    // Main function to perform heap sort
    void heapSort(vector<int>& arr) {
        int n = arr.size();
        
        // Build max heap (rearrange array)
        for (int i = n/2 - 1; i >= 0; i--)
            heapify(arr, n, i);
        
        // One by one extract elements from heap
        for (int i = n-1; i > 0; i--) {
            // Move current root to end
            swap(arr[0], arr[i]);
            
            // Call heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

private:
    // To heapify a subtree rooted with node i
    // n is size of heap
    void heapify(vector<int>& arr, int n, int i) {
        int largest = i; // Initialize largest as root
        int left = 2*i + 1;
        int right = 2*i + 2;
        
        // If left child is larger than root
        if (left < n && arr[left] > arr[largest])
            largest = left;
        
        // If right child is larger than current largest
        if (right < n && arr[right] > arr[largest])
            largest = right;
        
        // If largest is not root
        if (largest != i) {
            swap(arr[i], arr[largest]);
            
            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }
};
