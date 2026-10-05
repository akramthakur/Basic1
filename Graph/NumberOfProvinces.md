# Number of Provinces - Solution

## Problem Statement
There are `n` cities. Some of them are connected, while some are not. Given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `i-th` city and the `j-th` city are directly connected, and `isConnected[i][j] = 0` otherwise, return the total number of provinces (connected components).

## Step-by-Step Logic

### Connected Components in Adjacency Matrix:
1. **Convert Matrix to Adjacency List**: 
   - Transform the adjacency matrix into adjacency list representation
   - Skip self-connections (i != j)
2. **DFS Traversal**:
   - Perform DFS from each unvisited city
   - Each complete DFS covers one province (connected component)
3. **Count Provinces**:
   - Increment counter for each new DFS start
   - All cities reachable from start belong to same province

## Complexity Analysis

### Time Complexity: **O(n²)**
- **O(n²)** for processing the n x n adjacency matrix
- **O(n + e)** for DFS traversal (e = number of edges)
- In worst case, e = O(n²) for complete graph

### Space Complexity: **O(n²)**
- **O(n²)** for adjacency list in worst case (complete graph)
- **O(n)** for visited array
- **O(n)** for recursion stack

## Final Code with Comments

```cpp
class Solution {
public:
    // DFS helper function to traverse connected component
    void dfss(int start, vector<vector<int>> &adj, vector<int>& vis) {
        vis[start] = 1;  // Mark current city as visited
        
        // Visit all connected cities
        for(auto it : adj[start]) {
            if(!vis[it]) {
                dfss(it, adj, vis);  // Recursively visit unconnected cities
            }
        }
    }
    
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        
        // Build adjacency list from adjacency matrix
        vector<vector<int>> adj(n);
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                // If cities are connected and not the same city
                if(isConnected[i][j] == 1 && i != j) {
                    adj[i].push_back(j);  // Add j to i's connections
                    adj[j].push_back(i);  // Add i to j's connections (undirected)
                }
            }
        }
        
        // Visited array to track visited cities
        vector<int> vis(n, 0);
        int ans = 0;  // Counter for provinces
        
        // Iterate through all cities
        for(int i = 0; i < n; i++) {
            // If city not visited, it's a new province
            if(!vis[i]) {
                // Perform DFS to mark entire province
                dfss(i, adj, vis);
                ans++;  // Increment province count
            }
        }
        
        return ans;
    }
};
