# Detect Cycle in Directed Graph (Kahn's Algorithm) - Solution

## Problem Statement
Given a directed graph with `V` vertices and a list of edges, determine if the graph contains any cycle.

## Step-by-Step Logic

### Algorithm:
1. **Kahn's Algorithm (Topological Sort)**: 
   - Compute in-degree for each vertex
   - Start with vertices having 0 in-degree
   - Process vertices, reduce in-degree of neighbors
   - If count of processed vertices < total vertices → cycle exists

### Key Insight:
- In a Directed Acyclic Graph (DAG), topological ordering exists
- If we cannot process all vertices (some remain with non-zero in-degree), cycle exists
- Self-loops (u == v) are immediate cycles

## Complexity Analysis

### Time Complexity: **O(V + E)**
- Building adjacency list: O(E)
- Computing in-degrees: O(E)
- Queue processing: O(V + E)

### Space Complexity: **O(V + E)**
- Adjacency list: O(E)
- In-degree array: O(V)
- Queue: O(V)

## Final Code with Comments

```cpp
class Solution {
  public:
    bool isCyclic(int V, vector<vector<int>> &edges) {
        // Build adjacency list and compute in-degrees
        vector<vector<int>> adj(V);
        vector<int> degree(V, 0);  // in-degree array
        
        queue<int> qu;
        int count = 0;  // count of processed vertices
        
        // Process each edge
        for(auto &i : edges) {
            int u = i[0], v = i[1];
            
            // Self-loop detection
            if(u == v) return true;
            
            degree[v]++;  // v has incoming edge from u
            adj[u].push_back(v);
        }
        
        // Find all vertices with 0 in-degree (no dependencies)
        for(int i = 0; i < V; i++) {
            if(degree[i] == 0) {
                qu.push(i);
                count++;
            }
        }
        
        // Process vertices in topological order
        while(!qu.empty()) {
            int curr = qu.front();
            qu.pop();
            
            // Reduce in-degree of all neighbors
            for(auto neighbor : adj[curr]) {
                degree[neighbor]--;
                // If in-degree becomes 0, add to queue
                if(degree[neighbor] == 0) {
                    qu.push(neighbor);
                    count++;
                }
            }
        }
        
        // If count < V, some vertices couldn't be processed (cycle exists)
        return (count < V);
    }
};
