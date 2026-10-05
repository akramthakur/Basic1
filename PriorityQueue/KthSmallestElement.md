# Kth Smallest Element in an Array - Solution

## Problem Statement
Given an integer array `arr` and an integer `k`, return the kth smallest element in the array.

## Step-by-Step Logic

### Max-Heap Approach:
1. **Custom Comparator**: Create max-heap (largest element at top)
2. **Initial Population**: Add first k elements to heap
3. **Selective Replacement**: For remaining elements, replace heap top if current element is smaller
4. **Final Result**: Heap top contains kth smallest element

## Complexity Analysis

### Time Complexity: **O(n log k)**
- Building initial heap: O(k log k)
- Processing remaining n-k elements: O((n-k) log k)
- Total: O(n log k)

### Space Complexity: **O(k)**
- Max-heap stores k elements
- Optimal for large n, small k

## Final Code with Comments

```cpp
class Solution {
public:
    // Custom comparator for max-heap
    struct Compare {
        bool operator()(int &a, int &b) {
            return a < b;  // Max-heap: larger elements have higher priority
        }
    };
    
    int kthSmallest(vector<int> &arr, int k) {
        // Max-heap to maintain k smallest elements
        priority_queue<int, vector<int>, Compare> que;
        int i = 0;
        
        // Add first k elements to heap
        while(i < k) {
            que.push(arr[i]);
            i++;
        }
        
        // Process remaining elements
        while(i < arr.size()) {
            // If current element is smaller than largest in heap
            if(arr[i] < que.top()) {
                que.pop();           // Remove largest
                que.push(arr[i]);    // Add current smaller element
            }
            i++;
        }
        
        // Top of max-heap is kth smallest element
        return que.top();
    }
};
