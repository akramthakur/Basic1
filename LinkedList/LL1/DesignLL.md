# Design Linked List - Solution

## Problem Statement
Implement the `MyLinkedList` class with singly linked list operations:
- `get(index)`
- `addAtHead(val)`
- `addAtTail(val)`
- `addAtIndex(index, val)`
- `deleteAtIndex(index)`

## Step-by-Step Logic

### 1. Node Structure & Initialization
- **Node class**: Stores value and next pointer
- **MyLinkedList**: Maintains head pointer and size counter

### 2. Get Operation
- Check index validity
- Traverse to index and return value
- Return -1 for invalid index

### 3. Add at Head
- Create new node
- Point new node to current head
- Update head to new node
- Increment size

### 4. Add at Tail
- Create new node
- Traverse to last node
- Link last node to new node
- Handle empty list case
- Increment size

### 5. Add at Index
- Handle edge cases (index 0 and index = size)
- Traverse to node before target position
- Insert new node in between
- Increment size

### 6. Delete at Index
- Handle head deletion separately
- Traverse to node before target position
- Bypass the node to be deleted
- Decrement size

## Complexity Analysis

### Time Complexity:
- **get()**: O(n) - worst case traversal
- **addAtHead()**: O(1) - constant time
- **addAtTail()**: O(n) - traversal to end
- **addAtIndex()**: O(n) - traversal to index
- **deleteAtIndex()**: O(n) - traversal to index

### Space Complexity: **O(n)**
- n nodes stored for n elements
- O(1) extra space per operation

## Final Code with Comments

```cpp
class Node {
public:
    int val;
    Node* next;
    Node(int x) {
        val = x;
        next = nullptr;
    }
};

class MyLinkedList {
private:
    int size = 0;
    Node* head = nullptr;
    
public:
    MyLinkedList() {
        // Constructor - initialize empty list
    }
    
    int get(int index) {
        // Check if index is valid
        if (index >= size || index < 0) {
            return -1;
        }
        // Traverse to the index
        Node* ptr = head;
        for (int i = 0; i < index; i++) {
            ptr = ptr->next;
        }
        return ptr->val;
    }
    
    void addAtHead(int val) {
        Node* ptr = new Node(val);
        ptr->next = head;  // New node points to current head
        head = ptr;        // Update head to new node
        size++;
    }
    
    void addAtTail(int val) {
        Node* ptr = new Node(val);
        if (head == nullptr) {
            // Empty list - new node becomes head
            head = ptr;
        } else {
            // Traverse to last node
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = ptr;  // Link last node to new node
        }
        size++;
    }
    
    void addAtIndex(int index, int val) {
        // Check index validity
        if (index < 0 || index > size) return;
        
        if (index == 0) {
            addAtHead(val);
            return;
        } else if (index == size) {
            addAtTail(val);
            return;
        } else {
            Node* node = new Node(val);
            Node* cur = head;
            // Traverse to node before insertion point
            for (int i = 0; i < index - 1; i++) {
                cur = cur->next;
            }
            node->next = cur->next;  // New node points to next node
            cur->next = node;        // Current node points to new node
            size++;
        }
    }
    
    void deleteAtIndex(int index) {
        // Check index validity
        if (index >= size || index < 0) return;
        
        size--;
        if (index == 0) {
            // Delete head - move head to next node
            head = head->next;
            return;
        }
        
        Node* curr = head;
        // Traverse to node before deletion point
        for (int i = 0; i < index - 1; i++) {
            curr = curr->next;
        }
        // Bypass the node to be deleted
        curr->next = curr->next->next;
    }
};
