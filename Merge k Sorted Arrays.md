## 01. Merge k Sorted Arrays

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/merge-k-sorted-arrays/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a 2D matrix mat[][] of size n x m. Each row in the matrix is sorted in non-decreasing order, merge all the rows and return a single sorted array that contains all the elements of the matrix.

#### Examples

##### Example 1

- **Input:**
```text
mat[][] = [[1, 3, 5, 7], [2, 4, 6, 8], [0, 9, 10, 11]]Output: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```
- **Explanation:** Merging all elements from the 3 sorted arrays and sorting them results in: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11].

##### Example 2

- **Input:**
```text
mat[][] = [[1, 2, 3, 4], [2, 2, 3, 4], [5, 5, 6, 6], [7, 8, 9, 9]]Output: [1, 2, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 8, 9, 9]
```
- **Explanation:** Merging all elements from the 4 sorted arrays and sorting them results in:[1, 2, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 8, 9, 9]

#### Constraints

- **1.** `1 ≤ n * m ≤ 10⁵⁰ ≤ mat[i][j] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(k*log(n)), k = total no. of elementsAuxiliary Space: O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 02:32:19
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> mergeArrays(vector<vector<int>> &a) {
        int n = a.size();
        int m = a[0].size();
        vector<int> ans;

        // Helper lambda
        auto pb = [&](const int& v) { ans.push_back(v); };

        // Min-heap definition
        priority_queue<pair<int, pair<int, int>>, 
                       vector<pair<int, pair<int, int>>>, 
                       greater<pair<int, pair<int, int>>>> pq;

        // Insert the first element of each row
        for(int i = 0; i < n; i++) {
            pq.push({a[i][0], {i, 0}}); 
        }

        while(!pq.empty()) {
            int x = pq.top().first;
            auto [r, c] = pq.top().second; // Correct C++17 structured binding
            pq.pop(); // Pop from the priority queue, not the lambda

            pb(x);

            // Push the next element of the same row if it exists
            if(c + 1 < m) {
                pq.push({a[r][c + 1], {r, c + 1}});
            }
        }
        return ans;
    }
};
```

*Generated on: 8/18/2026, 2:32:44 AM*