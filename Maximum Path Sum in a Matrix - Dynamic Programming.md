## 01. Maximum Path Sum in a Matrix | Dynamic Programming

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/path-in-matrix3805/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** You are given a matrix mat[][] of size n x m where each element is a positive integer. Starting from any cell in the first row, you are allowed to move to the next row, but with specific movement constraints. From any cell (r, c) in the current row, you can move to any of the three possible positions :
(r+1, c-1) — move diagonally to the left.
(r+1, c) — move directly down.
(r+1, c+1) — move diagonally to the right.
Find the maximum sum of any path starting from any column in the first row and ending at any column in the last row, following the above movement constraints.

#### Examples

##### Example 1

- **Input:**
```text
mat[][] = [[3, 6, 1], [2, 3, 4], [5, 5, 1]]
```
- **Output:**
```text
15 Explaination: The best path is (0, 1) - > (1, 2) - > (2, 1). It gives the maximum sum as 15.
```

##### Example 2

- **Input:**
```text
mat[][] = [[2, 1, 1], [1, 2, 2]]
```
- **Output:**
```text
4 Explaination: The best path is (0, 0) - > (1, 1). It gives the maximum sum as 4.
```

##### Example 3

- **Input:**
```text
mat[][] = [[25]]
```
- **Output:**
```text
25 Explaination: (0, 0) is the only cell in mat[][], so maximum path sum will be 25.
```

#### Constraints

- **1.** `1 ≤ mat.size() ≤ 5001 ≤ mat[i].size() ≤ 5001 ≤ mat[i][j] ≤ 1000`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * m)
- **Expected Auxiliary Space Complexity:** O(n * m)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-19 01:55:12
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int maximumPath(vector<vector<int>>& mat) {
        int n = mat.size();
        int m = mat[0].size();

        // Start from the second row
        for (int i = 1; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                // Fetch the three possible paths from the previous row
                int up = mat[i-1][j];
                int left_diag = (j > 0) ? mat[i-1][j-1] : 0;
                int right_diag = (j < m - 1) ? mat[i-1][j+1] : 0;

                // Update the current cell with the maximum of the valid previous cells
                mat[i][j] += max({up, left_diag, right_diag});
            }
        }

        // Find the maximum value in the last row
        int max_sum = 0;
        for (int j = 0; j < m; ++j) {
            max_sum = max(max_sum, mat[n-1][j]);
        }

        return max_sum;
    }
};
```

*Generated on: 8/19/2026, 1:55:42 AM*