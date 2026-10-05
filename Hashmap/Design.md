# HashMap Implementation using Set - Solution Analysis

## Problem Statement
Design a HashMap without using any built-in hash table libraries using only standard library containers.

## Current Approach Issues

### Problems Identified:
1. **Inefficient Operations**: O(n) time for put, get, remove
2. **Linear Search**: Scanning entire set for key operations
3. **Wrong Data Structure**: Set is for unique elements, not key-value mapping

## Complexity Analysis

### Current Implementation:
- **put(key, value)**: O(n) - linear scan + O(log n) insert
- **get(key)**: O(n) - linear scan of entire set
- **remove(key)**: O(n) - linear scan + O(log n) erase
- **Space**: O(n) - stores all key-value pairs

## Optimized Solution

### Using Vector (Fixed Size) - O(1) average
```cpp
class MyHashMap {
    vector<list<pair<int, int>>> data;
    int size = 10000;
    
public:
    MyHashMap() : data(size) {}
    
    void put(int key, int value) {
        int index = key % size;
        auto& bucket = data[index];
        
        for(auto it = bucket.begin(); it != bucket.end(); it++) {
            if(it->first == key) {
                it->second = value;
                return;
            }
        }
        bucket.push_back({key, value});
    }
    
    int get(int key) {
        int index = key % size;
        auto& bucket = data[index];
        
        for(auto& p : bucket) {
            if(p.first == key) return p.second;
        }
        return -1;
    }
    
    void remove(int key) {
        int index = key % size;
        auto& bucket = data[index];
        
        for(auto it = bucket.begin(); it != bucket.end(); it++) {
            if(it->first == key) {
                bucket.erase(it);
                return;
            }
        }
    }
};
