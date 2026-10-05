# Hidato Puzzle Solver - Complete Implementation

## Problem Statement
Hidato is a logic puzzle where the goal is to fill a grid with consecutive numbers from 1 to N, connecting horizontally, vertically, or diagonally. The puzzle contains some pre-filled numbers and obstacles.

## Algorithm Overview

### Backtracking with Constraint Propagation:
1. **Start from number 1** and find consecutive numbers
2. **8-direction movement**: Can move in all 8 directions (like a king in chess)
3. **Constraint checking**: Ensure numbers are consecutive and follow connectivity rules
4. **Early pruning**: Stop exploring paths that violate constraints

## Complexity Analysis

### Time Complexity: **O(8^N)**
- In worst case, exponential but heavily pruned by constraints
- N = maximum number in the puzzle

### Space Complexity: **O(W × H)**
- Grid storage and neighbor tracking
- W = width, H = height of puzzle

## Code Structure Breakdown
```cpp

#include <bits/stdc++.h>
using namespace std;

struct node {
    int val;
    unsigned char neighbors;
};

class hSolver {
public:
    hSolver() {
        dx[0] = -1; dx[1] = 0; dx[2] = 1; dx[3] = -1; dx[4] = 1; dx[5] = -1; dx[6] = 0; dx[7] = 1;
        dy[0] = -1; dy[1] = -1; dy[2] = -1; dy[3] = 0; dy[4] = 0; dy[5] = 1; dy[6] = 1; dy[7] = 1;
    }

    void solve(vector<string>& puzz, int maxwid) {
        if (puzz.empty()) return;
        wid = maxwid;
        hei = static_cast<int>(puzz.size()) / wid;
        int len = wid * hei, c = 0;
        arr = new node[len];
        memset(arr, 0, len * sizeof(node));
        weHave = new bool[len + 1];
        memset(weHave, 0, len + 1);

        maxVal = 0; // <-- FIXED: use class variable instead of local `max`

        for (auto& str : puzz) {
            if (str == "*") {
                arr[c++].val = -1;
                continue;
            }
            arr[c].val = atoi(str.c_str());
            if (arr[c].val > 0) weHave[arr[c].val] = true;
            if (maxVal < arr[c].val) maxVal = arr[c].val;
            c++;
        }

        solveIt();

        c = 0;
        for (auto& str : puzz) {
            if (str == ".") {
                ostringstream o;
                o << arr[c].val;
                str = o.str();
            }
            c++;
        }

        delete[] arr;
        delete[] weHave;
    }

private:
    bool search(int x, int y, int w) {
        if (w > maxVal) return true;
        node* n = &arr[x + y * wid];
        n->neighbors = getNeighbors(x, y);

        if (weHave[w]) {
            for (int d = 0; d < 8; d++) {
                if (n->neighbors & (1 << d)) {
                    int a = x + dx[d], b = y + dy[d];
                    if (arr[a + b * wid].val == w)
                        if (search(a, b, w + 1)) return true;
                }
            }
            return false;
        }

        for (int d = 0; d < 8; d++) {
            if (n->neighbors & (1 << d)) {
                int a = x + dx[d], b = y + dy[d];
                if (arr[a + b * wid].val == 0) {
                    arr[a + b * wid].val = w;
                    if (search(a, b, w + 1)) return true;
                    arr[a + b * wid].val = 0;
                }
            }
        }
        return false;
    }

    unsigned char getNeighbors(int x, int y) {
        unsigned char c = 0;
        int m = -1, a, b;
        for (int yy = -1; yy < 2; yy++) {
            for (int xx = -1; xx < 2; xx++) {
                if (!yy && !xx) continue;
                m++;
                a = x + xx;
                b = y + yy;
                if (a < 0 || b < 0 || a >= wid || b >= hei)
                    continue;
                if (arr[a + b * wid].val > -1) c |= (1 << m);
            }
        }
        return c;
    }

    void solveIt() {
        int x, y;
        findStart(x, y);
        if (x < 0) {
            cout << "Can't find start" << endl;
            return;
        }
        search(x, y, 2);
    }

    void findStart(int& x, int& y) {
        for (int b = 0; b < hei; b++) {
            for (int a = 0; a < wid; a++) {
                if (arr[a + wid * b].val == 1) {
                    x = a;
                    y = b;
                    return;
                }
            }
        }
        x = y = -1;
    }

    int wid, hei, maxVal;
    int dx[8], dy[8];
    node* arr;
    bool* weHave;
};

int main() {
    int wid;
    string p = ". 33 35 . . * * * . . 24 22 . * * * . . . 21 . . * * . 26 . 13 40 11 * * 27 . . . 9 . 1 * * * . . 18 . . * * * * * . 7 . . * * * * * * 5 .";
    wid = 8;

    istringstream iss(p);
    vector<string> puzz;
    copy(istream_iterator<string>(iss), istream_iterator<string>(), back_inserter(puzz));

    hSolver s;
    s.solve(puzz, wid);

    int c = 0;
    for (auto& str : puzz) {
        if (str != "*" && str != ".") {
            if (atoi(str.c_str()) < 10) cout << "0";
            cout << str << " ";
        } else
            cout << "   ";
        if (++c >= wid) {
            cout << endl;
            c = 0;
        }
    }
    cout << endl << endl;
    return 0;
}

