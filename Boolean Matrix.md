## 01. Boolean Matrix

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/boolean-matrix-problem-1587115620/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a boolean matrix mat[], where each cell contains either 0 or 1, modify it such that if a matrix cell matrix[i][j] is 1 then all the cells in its i^th row and j^th column will become 1.

#### Examples

##### Example 1

- **Input:**
```text
mat[][] = [[1, 0], [0, 0]]
```
- **Output:**
```text
[[1, 1], [1, 0]]
```
- **Explanation:** Only cell that has 1 is at (0,0) so all cells in row 0 are modified to 1 and all cells in column 0 are modified to 1.

##### Example 2

- **Input:**
```text
mat[][] = [[1, 0, 0], [1, 0, 0], [1, 0, 0], [0, 0, 0]]
```
- **Output:**
```text
[[1, 1, 1], [1, 1, 1], [1, 1, 1], [1, 0, 0]]
```
- **Explanation:** The position of cells that have 1 in the original matrix are (0, 0), (1, 0) and (2, 0). Therefore, all cells in row 0, 1, 2 are and column 0 are modified to 1.

##### Example 3

- **Input:**
```text
mat[][] = [[0, 0], [0, 0]]
```
- **Output:**
```text
[[0, 0], [0, 0]]
```
- **Explanation:** There is no cell that contains 1, so mat[] will remain the same.

#### Constraints

- **1.** `1 ≤ mat.size(), mat[0].size() ≤ 10³⁰ ≤ mat[i][j] ≤ 1`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 23:40:08
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    void booleanMatrix(vector<vector<int>>& mat) {
        int r = mat.size();
        if (r == 0) return;
        int c = mat[0].size();

        bool firstRow = false, firstCol = false;

        // 1. Check if the first row has any 1s
        for (int j = 0; j < c; j++) {
            if (mat[0][j] == 1) {
                firstRow = true;
                break;
            }
        }

        // 2. Check if the first column has any 1s
        for (int i = 0; i < r; i++) {
            if (mat[i][0] == 1) {
                firstCol = true;
                break;
            }
        }

        // 3. Use the first row and first column to mark which rows and columns should be 1
        for (int i = 1; i < r; i++) {
            for (int j = 1; j < c; j++) {
                if (mat[i][j] == 1) {
                    mat[i][0] = 1;
                    mat[0][j] = 1;
                }
            }
        }

        // 4. Update the matrix elements (excluding the first row and first column) based on the marks
        for (int i = 1; i < r; i++) {
            for (int j = 1; j < c; j++) {
                if (mat[i][0] == 1 || mat[0][j] == 1) {
                    mat[i][j] = 1;
                }
            }
        }

        // 5. Update the first row if needed
        if (firstRow) {
            for (int j = 0; j < c; j++) {
                mat[0][j] = 1;
            }
        }

        // 6. Update the first column if needed
        if (firstCol) {
            for (int i = 0; i < r; i++) {
                mat[i][0] = 1;
            }
        }
    }
};
```

*Generated on: 8/18/2026, 11:40:38 PM*