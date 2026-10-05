# String Reversal using Stack - Solution

## Problem Statement
Implement a stack using an array and use it to reverse a string by pushing all characters onto the stack and then popping them off.

## Step-by-Step Logic

### Stack Operations:
1. **Push**: Add element to top of stack
2. **Pop**: Remove and return top element from stack
3. **isEmpty**: Check if stack has no elements
4. **isFull**: Check if stack has reached maximum capacity

### String Reversal Logic:
1. **Push Phase**: Push each character of input string onto stack
2. **Pop Phase**: Pop characters from stack to build reversed string
3. **LIFO Property**: Last In First Out nature of stack reverses the order

## Complexity Analysis

### Time Complexity: **O(n)**
- Push n characters: O(n)
- Pop n characters: O(n)
- Total: O(2n) = O(n)

### Space Complexity: **O(n)**
- Stack array of fixed size: O(101)
- Reversed string storage: O(n)

## Final Code with Comments

```cpp
#include <bits/stdc++.h>
using namespace std;

#define STACK_MAX_SIZE 101
char stackArray[STACK_MAX_SIZE];
int stackTop = -1;

bool isStackEmpty() {
    return stackTop == -1;
}

bool isStackFull() {
    return stackTop >= STACK_MAX_SIZE - 1;
}

void pushToStack(char element) {
    // Check if stack is full
    if(isStackFull()) {
        cout << "Stack is full" << endl;
        return;
    }
    // Add element at top position and update top
    stackArray[stackTop + 1] = element;
    stackTop++;
}

char popFromStack() {
    // Check if stack is empty
    if(isStackEmpty()) {
        cout << "Stack is empty" << endl;
        return -1;
    }
    // Return top element and decrement top
    stackTop--;
    return stackArray[stackTop + 1];
}

int main() {
    string inputString = "Hello, World!";
    int inputLength = inputString.length();

    // Push each character onto the stack
    for (int i = 0; i < inputLength; i++) {
        char currentChar = inputString[i];
        pushToStack(currentChar);
    }

    // Pop characters to build reversed string
    string reversedString;
    while (!isStackEmpty()) {
        reversedString.push_back(popFromStack());
    }
    
    cout << reversedString << "\n";
    return 0;
}
