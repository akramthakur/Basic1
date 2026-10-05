# Graph Coloring (M-Coloring) - Solution

## Problem Statement
Given an undirected graph and an integer `m`, determine if the graph can be colored with at most `m` colors such that no two adjacent vertices share the same color.

## Step-by-Step Logic

### Backtracking Approach:
1. **Graph Representation**: Convert edge list to adjacency list
2. **Color Assignment**: Try colors 1 to m for each vertex
3. **Constraint Checking**: Ensure no adjacent vertices have same color
4. **Backtracking**: If coloring fails, undo assignment and try next color

## Algorithm Details

### Key Functions:
- **isSafe()**: Checks if color `c` can be assigned to vertex `node`
- **dfs()**: Recursive backtracking to try all color combinations
- **graphColoring()**: Main function to initialize and start coloring

### Coloring Process:
- **Vertex Order**: Process vertices from 0 to v-1 sequentially
- **Color Try**: For each vertex, try colors 1 through m
- **Backtrack**: If no valid color found, backtrack to previous vertex

## Complexity Analysis

### Time Complexity: **O(m^v)**
- **Worst Case**: Try m colors for each of v vertices
- **Backtracking**: Prunes invalid paths early
- **Practical**: Much better with constraint propagation

### Space Complexity: **O(v + e)**
- **Adjacency List**: O(v + e)
- **Color Array**: O(v)
- **Recursion Stack**: O(v)

## Final Code with Comments

```cpp
class Solution {
public:
    // Check if color 'c' can be assigned to vertex 'node'
    bool isSafe(int c, int node, vector<int>& color, vector<vector<int>>& adjlist) {
        // Check all adjacent vertices
        for(auto it : adjlist[node]) {
            if(color[it] == c) return false;
        }
        return true;
    }
    
    // Backtracking DFS for graph coloring
    bool dfs(vector<vector<int>>& adj, int m, int v, vector<int>& color, int node) {
        // Base case: all vertices colored
        if(node == v) return true;
        
        // Try all colors from 1 to m
        for(int i = 1; i <= m; i++) {
            if(isSafe(i, node, color, adj)) {
                color[node] = i;  // Assign color
                
                // Recursively color remaining vertices
                if(dfs(adj, m, v, color, node + 1)) 
                    return true;
                
                color[node] = 0;  // Backtrack
            }
        }
        return false;
    }
    
    bool graphColoring(int v, vector<vector<int>> &edges, int m) {
        // Build adjacency list
        vector<vector<int>> adj(v);
        for(auto it : edges) {
            adj[it[0]].push_back(it[1]);
            adj[it[1]].push_back(it[0]);
        }
        
        // Initialize color array (-1 represents uncolored)
        vector<int> color(v, -1);
        
        // Start coloring from vertex 0
        return dfs(adj, m, v, color, 0);
    }
};
