## 01. Minimum Swaps to Sort

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/minimum-swaps/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an array arr[] of distinct elements. Find the minimum number of swaps required to sort the array in strictly increasing order.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [2, 8, 5, 4]
```
- **Output:**
```text
1
```
- **Explanation:** Swap 8 with 4 to get the sorted array.

##### Example 2

- **Input:**
```text
arr[] = [10, 19, 6, 3, 5]
```
- **Output:**
```text
2
```
- **Explanation:** Swap 10 with 3 and 19 with 5 to get the sorted array.

##### Example 3

- **Input:**
```text
arr[] = [1, 3, 4, 5, 6]
```
- **Output:**
```text
0
```
- **Explanation:** Input array is already sorted.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n log n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-15 17:24:32
- **Status:** Correct
- **Marks:** 4

```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    int minSwaps(vector<int>& arr) {
        int n = arr.size();
        
        // Store the elements along with their initial indices
        vector<pair<int, int>> vec(n);
        for (int i = 0; i < n; i++) {
            vec[i] = {arr[i], i};
        }
        
        // Sort the vector by element values
        sort(vec.begin(), vec.end());
        
        // To keep track of visited elements
        vector<bool> visited(n, false);
        int swaps = 0;
        
        for (int i = 0; i < n; i++) {
            // If the element is already visited or is already in the correct sorted position
            if (visited[i] || vec[i].second == i) {
                continue;
            }
            
            // Find the size of the cycle
            int cycle_size = 0;
            int j = i;
            
            while (!visited[j]) {
                visited[j] = true;
                // Move to the index where this element originally came from
                j = vec[j].second;
                cycle_size++;
            }
            
            // If there is a cycle of size k, we need (k - 1) swaps
            if (cycle_size > 1) {
                swaps += (cycle_size - 1);
            }
        }
        
        return swaps;
    }
};
```

*Generated on: 7/15/2026, 5:24:52 PM*