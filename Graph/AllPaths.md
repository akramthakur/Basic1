# All Paths From Source to Target - Solution

## Problem Statement
Given a directed acyclic graph (DAG) of `n` nodes labeled from `0` to `n-1`, find all possible paths from node `0` to node `n-1` and return them in any order.

The graph is given as an adjacency list where `graph[i]` is a list of all nodes you can visit from node `i`.

## Step-by-Step Logic

### Algorithm:
1. **DFS with Backtracking**: Use depth-first search to explore all paths
2. **Path Tracking**: Maintain current path and add to result when target is reached
3. **Backtracking**: Remove current node after exploring all paths from it

### Key Insight:
- Since it's a DAG, no cycles exist, so we don't need visited array
- We can explore all paths systematically using DFS with backtracking
- The target is always the last node `n-1`

## Complexity Analysis

### Time Complexity: **O(2^n × n)**
- In worst case, there can be 2^(n-2) paths in a complete DAG
- Each path can have up to n nodes

### Space Complexity: **O(n)**
- Recursion stack depth: O(n)
- Path storage: O(n) per path in recursion
- Output space not counted as extra space

## Final Code with Comments

```cpp
class Solution {
public:
    void dfs(vector<vector<int>>& graph, int current, int target, 
             vector<int>& path, vector<vector<int>>& res) {
        
        // Add current node to path
        path.push_back(current);
        
        // If we reached the target, save the path
        if (current == target) {
            res.push_back(path);
        } else {
            // Explore all neighbors
            for (int neighbor : graph[current]) {
                dfs(graph, neighbor, target, path, res);
            }
        }
        
        // Backtrack: remove current node from path
        path.pop_back();
    }
    
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> res;  // Store all paths
        vector<int> path;         // Current path being explored
        int target = graph.size() - 1;  // Target node is always n-1
        
        dfs(graph, 0, target, path, res);
        return res;
    }
};
