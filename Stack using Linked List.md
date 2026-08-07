## 01. Stack using Linked List

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/implement-stack-using-linked-list/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Implement a Stack using a Linked List. The stack has dynamic size and can grow until memory is available.The Stack must support the following operations:
(i) push(x): Insert an element x at the top of the stack.(ii) pop(): Remove the element from the top of the stack.(iii) peek(): Return top element if not empty, else -1.(iv) isEmpty(): Return true if the stack is empty else return false.(v) size(): Return the number of elements currently in the stack.
There will be a sequence of queries queries[][] in numeric form:
1 x : Call push(x)
2: Call pop()
3: Call peek()
4: Call isEmpty()
5: Call size()
Implement only the functions push, pop, peek, isEmpty, and size. The driver code handles input and output.

#### Examples

##### Example 1

- **Input:**
```text
q = 7, queries[][] = [[1, 5], [1, 3], [1, 4], [3], [2], [5], [4]]
```
- **Output:**
```text
[4, 2, false]
```
- **Explanation:** Queries on queue are as follows:push(5): Insert 5 at the top of the stack.push(3): Insert 3 at the top of the stack.push(4): Insert 4 at the top of the stack.peek(): Return the top element i.e 4.pop(): Remove the top element 4 from the stack.size(): Stack contains 2 elements return 2.isEmpty(): Stack is not empty return false.

##### Example 2

- **Input:**
```text
q = 4, queries[][] = [[4], [3], [1, 10], [5]]
```
- **Output:**
```text
[true, -1, 1]
```
- **Explanation:** Queries on queue are as follows:isEmpty(): Stack is empty return true.peek(): Stack is empty return -1.push(10): Insert 10 at the top of the stack.size(): Stack contains 1 element return 1.

#### Constraints

- **1.** `1 ≤ number of query ≤ 10³⁰ ≤ x ≤ 10⁵`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(1)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-13 17:40:09
- **Status:** Correct
- **Marks:** 2

```cpp
// Assuming the Node structure is defined as follows by the driver code:
/*
struct Node {
    int data;
    Node* next;
    Node(int a) {
        data = a;
        next = NULL;
    }
};
*/

class myStack {
private:
    Node* topNode;
    int sz;

public:
    myStack() {
        topNode = NULL;
        sz = 0;
    }

    // Returns true if the stack is empty, else false
    bool isEmpty() {
        return topNode == NULL;
    }

    // Adds an element x at the top of the stack
    void push(int x) {
        Node* newNode = new Node(x);
        newNode->next = topNode;
        topNode = newNode;
        sz++;
    }

    // Removes the top element of the stack
    void pop() {
        if (isEmpty()) {
            return;
        }
        Node* temp = topNode;
        topNode = topNode->next;
        delete temp;
        sz--;
    }

    // Returns the top element of the stack. If empty, return -1
    int peek() {
        if (isEmpty()) {
            return -1;
        }
        return topNode->data;
    }

    // Returns the number of elements currently in the stack
    int size() {
        return sz;
    }
};
```

*Generated on: 7/13/2026, 5:40:36 PM*