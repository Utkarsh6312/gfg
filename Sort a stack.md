## 01. Sort a stack

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/sort-a-stack/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a stack of integers st[]. Sort the stack in ascending order (smallest element at the bottom and largest at the top).

#### Examples

##### Example 1

- **Input:**
```text
st[] = [41, 3, 32, 2, 11]Output: [41, 32, 11, 3, 2]Explanation: After sorting, the smallest element (2) is at the bottom and the largest element (41) is at the top.
```

##### Example 2

- **Input:**
```text
st[] = [3, 2, 1]Output: [3, 2, 1]Explanation: The stack is already sorted in ascending order.
```

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (2)

#### Solution 1 (C++)

- **Submitted:** 2026-07-15 17:45:19
- **Status:** Correct
- **Marks:** 0

```cpp
#include <stack>

using namespace std;

class Solution {
private:
    // Helper function to insert an element into its sorted position in the stack
    void sortedInsert(stack<int>& st, int element) {
        // Base case: if stack is empty or the top element is smaller than/equal to 'element'
        if (st.empty() || st.top() <= element) {
            st.push(element);
            return;
        }

        // If top is greater, pop it and find the correct spot recursively
        int temp = st.top();
        st.pop();
        
        sortedInsert(st, element);

        // Put the popped element back on top
        st.push(temp);
    }

public:
    void sortStack(stack<int>& st) {
        // Base case: if stack is empty, it is already sorted
        if (st.empty()) {
            return;
        }

        // Remove the top element
        int temp = st.top();
        st.pop();

        // Recursively sort the remaining stack
        sortStack(st);

        // Insert the popped element back in its sorted position
        sortedInsert(st, temp);
    }
};
```

#### Solution 2 (C++)

- **Submitted:** 2026-07-15 17:30:18
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    void sortStack(stack<int> &st) {
        // code here
        vector<int> a;
        while(!st.empty()){
            a.push_back(st.top());st.pop();
        }sort(a.begin(),a.end());
        for(auto i: a)st.push(i);
    }
};
```

*Generated on: 7/15/2026, 5:45:40 PM*