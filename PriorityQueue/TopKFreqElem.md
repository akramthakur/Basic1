# Top K Frequent Elements - Solution

## Problem Statement
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements.

## Step-by-Step Logic

### Min-Heap Approach:
1. **Count Frequencies**: Use hash map to count occurrences of each element
2. **Maintain Top K**: Use min-heap to keep track of k most frequent elements
3. **Heap Management**: 
   - Add first k elements directly
   - For remaining elements, replace heap root if current frequency is higher
4. **Extract Result**: Pop all elements from heap to get final result

## Complexity Analysis

### Time Complexity: **O(N log K)**
- **O(N)** for frequency counting
- **O(U log K)** for heap operations (U = unique elements)
- Overall: **O(N log K)**

### Space Complexity: **O(N + K)**
- **O(N)** for hash map storage
- **O(K)** for min-heap storage

## Final Code with Comments

```cpp
class Solution {
public:
    struct Compare {
        bool operator()(pair<int,int>& a, pair<int,int>& b) {
            return a.second > b.second;  // Min-heap based on frequency
        }
    };
    
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // Step 1: Count frequencies using hash map
        unordered_map<int,int> map;
        for(int i: nums) {
            map[i]++;
        }
        
        // Step 2: Use min-heap to maintain top k frequent elements
        priority_queue<pair<int,int>, vector<pair<int,int>>, Compare> que;
        int i = 0;
        
        // Step 3: Iterate through frequency map
        for(auto& [key,val]: map) {
            if(i < k) {
                // Add first k elements directly
                que.push({key,val});
            } else if(que.top().second < val) {
                // Replace if current frequency is higher than heap's minimum
                que.pop();
                que.push({key,val});
            }
            i++;
        }
        
        // Step 4: Extract results from heap
        vector<int> ans;
        while(!que.empty()) {
            ans.push_back(que.top().first);
            que.pop();
        }
        return ans;
    }
};
