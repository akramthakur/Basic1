# Kruskal's Algorithm - Minimum Spanning Tree Solution

## Problem Statement
Given a connected, undirected, and weighted graph with `V` vertices and `E` edges, find the minimum spanning tree (MST) weight using Kruskal's algorithm with Union-Find data structure.

## Step-by-Step Logic

### Kruskal's Algorithm Approach:
1. **Sort Edges**: Sort all edges by weight in non-decreasing order
2. **Union-Find**: Use Disjoint Set Union (DSU) to detect cycles
3. **Greedy Selection**: Add edges to MST if they don't form cycles
4. **Termination**: Stop when V-1 edges are selected (tree property)

## Algorithm Details

### Disjoint Set Operations:
- **FindUpar**: Path compression for efficient root finding
- **UnionByRank**: Union by rank to keep trees balanced
- **UnionBySize**: Alternative union by size approach

### MST Construction:
- **Edge Sorting**: O(E log E) to sort edges by weight
- **Cycle Detection**: O(α(V)) per edge using DSU
- **Edge Selection**: Add edge if vertices are in different sets

## Complexity Analysis

### Time Complexity: **O(E log E + E α(V))**
- **Edge Sorting**: O(E log E)
- **Union-Find Operations**: O(E α(V)) where α is inverse Ackermann
- **Total**: O(E log E) (dominated by sorting)

### Space Complexity: **O(V + E)**
- **Disjoint Set**: O(V) for parent, rank, size arrays
- **Edge Storage**: O(E) for sorted edges
- **Auxiliary**: O(1) for MST construction

## Final Code with Comments

```cpp
class DisjointSet {
    vector<int> Rank, Parent, Size;

public:
    DisjointSet(int n) {
        Rank.resize(n + 1, 0);
        Parent.resize(n + 1);
        Size.resize(n + 1, 1);
        // Initialize each node as its own parent
        for (int i = 0; i <= n; i++) {
            Parent[i] = i;
        }
    }

    // Find with path compression
    int FindUpar(int node) {
        if (Parent[node] == node) return node;
        return Parent[node] = FindUpar(Parent[node]); // Path compression
    }

    // Union by rank for balanced trees
    void UnionByRank(int u, int v) {
        int ulp_u = FindUpar(u);
        int ulp_v = FindUpar(v);

        if (ulp_u == ulp_v) return; // Already connected

        if (Rank[ulp_u] < Rank[ulp_v]) {
            Parent[ulp_u] = ulp_v;
        } else if (Rank[ulp_u] > Rank[ulp_v]) {
            Parent[ulp_v] = ulp_u;
        } else {
            Parent[ulp_v] = ulp_u;
            Rank[ulp_u]++;
        }
    }

    // Union by size as alternative
    void UnionBySize(int u, int v) {
        int ulp_u = FindUpar(u);
        int ulp_v = FindUpar(v);

        if (ulp_u == ulp_v) return;

        if (Size[ulp_u] < Size[ulp_v]) {
            Parent[ulp_u] = ulp_v;
            Size[ulp_v] += Size[ulp_u];
        } else {
            Parent[ulp_v] = ulp_u;
            Size[ulp_u] += Size[ulp_v];
        }
    }
};

class Solution {
public:
    int kruskalsMST(int V, vector<vector<int>> &edges) {
        DisjointSet ds(V);
        
        // Sort edges by weight in ascending order
        sort(edges.begin(), edges.end(),
            [](vector<int>& a, vector<int>& b) {
                return a[2] < b[2];
            }
        );

        int mstWeight = 0;
        
        // Process edges in sorted order
        for(auto edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int wt = edge[2];
            
            // If vertices are in different components, add edge to MST
            if (ds.FindUpar(u) != ds.FindUpar(v)) {
                ds.UnionByRank(u, v); 
                mstWeight += wt;
            }
        }
        
        return mstWeight;
    }
};
