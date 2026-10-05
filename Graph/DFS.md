# Depth-First Search (DFS) Traversal - Solution

## Problem Statement
Given the adjacency list representation of a connected undirected graph, perform DFS traversal starting from vertex 0 and return the order of visited vertices.

## Step-by-Step Logic

### DFS Algorithm:
1. **Initialize**:
   - Visited array to track visited vertices
   - Result list to store DFS order
   - Start from vertex 0
2. **Recursive DFS**:
   - Mark current vertex as visited
   - Add to result list
   - Recursively visit all unvisited neighbors
3. **Backtrack**: Automatically handled by recursion stack
4. **Terminate**: When all reachable vertices are visited

## Complexity Analysis

### Time Complexity: **O(V + E)**
- **O(V)** for processing each vertex once
- **O(E)** for processing all edges (each edge considered twice in undirected graph)
- **V** = number of vertices, **E** = number of edges

### Space Complexity: **O(V)**
- **O(V)** for visited array
- **O(V)** for recursion stack in worst case
- **O(V)** for result vector

## Final Code with Comments

```cpp
class Solution {
public:
    // Recursive DFS helper function
    void dfss(int start, vector<vector<int>> &adj, vector<int>& vis, vector<int>& list) {
        // Mark current node as visited
        vis[start] = 1;
        
        // Add current node to DFS result
        list.push_back(start);
        
        // Visit all adjacent vertices
        for(auto it : adj[start]) {
            // If neighbor not visited, recursively visit it
            if(!vis[it]) {
                dfss(it, adj, vis, list);
            }
        }
    }
    
    vector<int> dfs(vector<vector<int>>& adj) {
        int V = adj.size();  // Number of vertices
        
        // Visited array to track visited vertices
        vector<int> vis(V, 0);
        
        int start = 0;  // Start DFS from vertex 0
        
        // Result vector to store DFS order
        vector<int> list;
        
        // Start DFS traversal
        dfss(start, adj, vis, list);
        
        return list;
    }
};
