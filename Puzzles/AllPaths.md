# All Paths From Source to Target - Solution

## Problem Statement
Given a directed acyclic graph (DAG) of `n` nodes labeled from `0` to `n-1`, find all possible paths from node `0` to node `n-1` and return them in any order.

## Step-by-Step Logic

### Depth-First Search (DFS) with Backtracking Approach:
1. **Path Tracking**: Maintain current path during traversal
2. **Target Check**: When reaching target node `n-1`, save current path
3. **Neighbor Exploration**: Recursively visit all neighbors of current node
4. **Backtracking**: Remove current node from path before returning to explore other paths

## Algorithm Details

### DFS Function
- **Parameters**: 
  - `graph`: Adjacency list representation
  - `current`: Current node being visited
  - `target`: Destination node (`n-1`)
  - `path`: Current path being built
  - `res`: Result container for all valid paths

### Process
1. Add current node to path
2. If current node equals target, save path to results
3. Otherwise, recursively visit all neighbors
4. Backtrack by removing current node from path

## Complexity Analysis

### Time Complexity: **O(2^n × n)**
- In worst case, DAG can have exponentially many paths
- Each path copy takes O(n) time
- Upper bound: O(2^n × n)

### Space Complexity: **O(n)**
- Recursion stack depth: O(n)
- Path storage during DFS: O(n)
- Output space not counted in auxiliary space

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
            // Explore all neighbors recursively
            for (int neighbor : graph[current]) {
                dfs(graph, neighbor, target, path, res);
            }
        }
        
        // Backtrack: remove current node from path
        // This allows us to reuse the path vector for other branches
        path.pop_back();
    }
    
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> res;  // Store all result paths
        vector<int> path;         // Track current path during DFS
        
        // Start DFS from node 0 to node n-1
        dfs(graph, 0, graph.size() - 1, path, res);
        
        return res;
    }
};
