# Hamiltonian Path Check - Backtracking Solution

## Problem Statement
Given an undirected graph with `n` vertices and `m` edges, determine if there exists a Hamiltonian path - a path that visits each vertex exactly once.

## Step-by-Step Logic

### Backtracking Approach:
1. **Graph Representation**: Convert edge list to adjacency list
2. **DFS Exploration**: Try all possible paths starting from each vertex
3. **Path Tracking**: Maintain current path and visited set
4. **Termination Check**: Return true when path contains all n vertices
5. **Backtracking**: Unmark visited when backtracking

## Algorithm Details

### Key Components:
- **adj**: Adjacency list representation
- **vis**: Tracks visited vertices to avoid cycles
- **store**: Stores current path being explored
- **DFS**: Recursive backtracking to explore all paths

### Process Flow:
1. Start from each vertex as potential starting point
2. Mark current vertex visited and add to path
3. If path length equals n, Hamiltonian path found
4. Recursively visit all unvisited neighbors
5. Backtrack if current path doesn't lead to solution

## Complexity Analysis

### Time Complexity: **O(n! × n)**
- **Worst Case**: Try all permutations of vertices = O(n!)
- **Neighbor Check**: O(n) per recursive call
- **Total**: O(n! × n)

### Space Complexity: **O(n + m)**
- **Adjacency List**: O(n + m)
- **Visited Array**: O(n)
- **Path Storage**: O(n)
- **Recursion Stack**: O(n)

## Code with Detailed Comments

```cpp
class Solution {
public:
    bool dfs(int i, int n, vector<vector<int>>& adj, vector<bool>& vis, vector<int>& store) {
        // Mark current vertex as visited and add to path
        vis[i] = true;
        store.push_back(i);
        
        // Check if we found Hamiltonian path (visited all vertices)
        if(store.size() == n) {
            return true;
        }
        
        // Explore all neighbors
        for(int x : adj[i]) {
            if(!vis[x]) {
                // Recursively explore unvisited neighbor
                if(dfs(x, n, adj, vis, store)) {
                    return true;
                }
            }
        }
        
        // Backtrack: remove current vertex from path and mark unvisited
        vis[i] = false;
        store.pop_back();
        return false;
    }
    
    bool check(int n, int m, vector<vector<int>> edges) {
        // Build adjacency list (1-based indexing)
        vector<vector<int>> adj(n + 1);
        for(auto &v : edges) {
            adj[v[0]].push_back(v[1]);
            adj[v[1]].push_back(v[0]);
        }
        
        // Try starting from each vertex
        for(int i = 1; i <= n; i++) {
            vector<bool> vis(n + 1, false);
            vector<int> store;
            if(dfs(i, n, adj, vis, store)) {
                return true;
            }
        }
        return false;
    }
};
