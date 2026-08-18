## 01. Replace O's with X's

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/replace-os-with-xs0052/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a grid[][] of size n*m, where every element is either 'O' or 'X'. Replace all 'O' or a group of 'O' with 'X' that are surrounded by 'X'.
A 'O' (or a set of 'O') is considered to be surrounded by 'X' if there are 'X' at locations just below, just above, just left and just right of it.

#### Examples

##### Example 1

- **Input:**
```text
grid[][] = [['X', 'X', 'X', 'X'], ['X', 'O', 'X', 'X'], ['X', 'O', 'O', 'X'], ['X', 'O', 'X', 'X'], ['X', 'X', 'O', 'O']]Output: Explanation: We only changed those 'O' that are surrounded by 'X'
```

##### Example 2

- **Input:**
```text
grid[][] = [['X', 'O', 'X', 'X'], ['X', 'O', 'X', 'X'], ['X', 'O', 'O', 'X'], ['X', 'O', 'X', 'X'], ['X', 'X', 'O', 'O']]
```
- **Output:**
```text
Explanation: There's no 'O' that's surround by 'X'.
```

##### Example 3

- **Input:**
```text
grid[][] = [['X', 'X', 'X'], ['X', 'O', 'X'], ['X', 'X', 'X']]
```
- **Output:**
```text
[['X', 'X', 'X'], ['X', 'X', 'X'], ['X', 'X', 'X']]
```
- **Explanation:** There's only one 'O' that's surround by 'X'.

#### Constraints

- **1.** `1 ≤ grid.size() ≤ 1001 ≤ grid[0].size() ≤ 100`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * m)
- **Expected Auxiliary Space Complexity:** O(n * m)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-09 21:05:41
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
private:
    void dfs(int row, int col, vector<vector<char>>& grid, vector<vector<int>>& vis, int delRow[], int delCol[]) {
        vis[row][col] = 1;
        int n = grid.size();
        int m = grid[0].size();
        
        // Check all 4 directions
        for(int i = 0; i < 4; i++) {
            int nrow = row + delRow[i];
            int ncol = col + delCol[i];
            
            if(nrow >= 0 && nrow < n && ncol >= 0 && ncol < m && !vis[nrow][ncol] && grid[nrow][ncol] == 'O') {
                dfs(nrow, ncol, grid, vis, delRow, delCol);
            }
        }
    }

public:
    void fill(vector<vector<char>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        
        vector<vector<int>> vis(n, vector<int>(m, 0));
        int delRow[] = {-1, 0, +1, 0};
        int delCol[] = {0, +1, 0, -1};
        
        // Traverse first and last row
        for(int j = 0; j < m; j++) {
            // First row
            if(!vis[0][j] && grid[0][j] == 'O') {
                dfs(0, j, grid, vis, delRow, delCol);
            }
            // Last row
            if(!vis[n - 1][j] && grid[n - 1][j] == 'O') {
                dfs(n - 1, j, grid, vis, delRow, delCol);
            }
        }
        
        // Traverse first and last column
        for(int i = 0; i < n; i++) {
            // First column
            if(!vis[i][0] && grid[i][0] == 'O') {
                dfs(i, 0, grid, vis, delRow, delCol);
            }
            // Last column
            if(!vis[i][m - 1] && grid[i][m - 1] == 'O') {
                dfs(i, m - 1, grid, vis, delRow, delCol);
            }
        }
        
        // If 'O' is unvisited, it is surrounded by 'X'
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(!vis[i][j] && grid[i][j] == 'O') {
                    grid[i][j] = 'X';
                }
            }
        }
    }
};
```

*Generated on: 8/9/2026, 9:07:14 PM*