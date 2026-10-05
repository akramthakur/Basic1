# Kth Largest Element in an Array - Solution

## Problem Statement
Given an integer array `nums` and an integer `k`, return the kth largest element in the array.

## Step-by-Step Logic

### Min-Heap Approach:
1. **Custom Comparator**: Create min-heap (smallest element at top)
2. **Initial Population**: Add first k elements to heap
3. **Selective Replacement**: For remaining elements, replace heap top if current element is larger
4. **Final Result**: Heap top contains kth largest element

## Complexity Analysis

### Time Complexity: **O(n log k)**
- Building initial heap: O(k log k)
- Processing remaining n-k elements: O((n-k) log k)
- Total: O(n log k)

### Space Complexity: **O(k)**
- Min-heap stores k elements
- Optimal for large n, small k

## Final Code with Comments

```cpp
class Solution {
public:
    // Custom comparator for min-heap
    struct Compare {
        bool operator()(int &a, int &b) {
            return a > b;  // Min-heap: smaller elements have higher priority
        }
    };
    
    int findKthLargest(vector<int>& nums, int k) {
        // Min-heap to maintain k largest elements
        priority_queue<int, vector<int>, Compare> que;
        int i = 0;
        
        // Add first k elements to heap
        while(i < k) {
            que.push(nums[i]);
            i++;
        }
        
        // Process remaining elements
        while(i < nums.size()) {
            // If current element is larger than smallest in heap
            if(nums[i] > que.top()) {
                que.pop();           // Remove smallest
                que.push(nums[i]);   // Add current larger element
            }
            i++;
        }
        
        // Top of min-heap is kth largest element
        return que.top();
    }
};
