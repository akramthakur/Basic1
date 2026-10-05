# Breadth-First Search (BFS) Traversal - Solution

## Problem Statement
Given the adjacency list representation of a connected undirected graph, perform BFS traversal starting from vertex 0 and return the order of visited vertices.

## Step-by-Step Logic

### BFS Algorithm:
1. **Initialize**: 
   - Visited array to track visited vertices
   - Queue for BFS traversal
   - Start from vertex 0
2. **Process Queue**:
   - Dequeue front vertex
   - Add to result list
   - Enqueue all unvisited neighbors
3. **Mark Visited**: Mark vertices as visited when enqueued
4. **Terminate**: When queue is empty

## Complexity Analysis

### Time Complexity: **O(V + E)**
- **O(V)** for processing each vertex once
- **O(E)** for processing all edges (each edge considered twice in undirected graph)
- **V** = number of vertices, **E** = number of edges

### Space Complexity: **O(V)**
- **O(V)** for visited array
- **O(V)** for queue in worst case
- **O(V)** for result vector

## Final Code with Comments

```cpp
class Solution {
public:
    vector<int> bfs(vector<vector<int>> &adj) {
        int V = adj.size();  // Number of vertices
        
        // Visited array to track visited vertices
        vector<int> vis(V, 0);
        
        // Mark starting vertex as visited
        vis[0] = 1;
        
        // Queue for BFS traversal
        queue<int> que;
        que.push(0);  // Start from vertex 0
        
        // Result vector to store BFS order
        vector<int> bfs;
        
        // Process until queue is empty
        while(!que.empty()) {
            // Get front vertex from queue
            int node = que.front();
            que.pop();
            
            // Add current node to BFS result
            bfs.push_back(node);
            
            // Visit all adjacent vertices
            for(auto it : adj[node]) {
                // If neighbor not visited, mark and enqueue
                if(!vis[it]) {
                    vis[it] = 1;      // Mark as visited
                    que.push(it);     // Add to queue
                }
            }
        }
        
        return bfs;
    }
};
