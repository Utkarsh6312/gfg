## 01. Distance of nearest cell having 1

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/distance-of-nearest-cell-having-1-1587115620/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a binary grid[][], where each cell contains either 0 or 1, find the distance of the nearest 1 for every cell in the grid.The distance between two cells (i_1, j_1) and (i_2, j_2) is calculated as |i_1 - i_2| + |j_1 - j_2|_. You need to return a matrix of the same size, where each cell (i, j) contains the minimum distance from grid[i][j] to the nearest cell having value 1.

> **Note:** It is guaranteed that there is at least one cell with value 1 in the grid.

#### Examples

##### Example 1

- **Input:**
```text
grid[][] = [[0, 1, 1, 0], [1, 1, 0, 0], [0, 0, 1, 1]]
```
- **Output:**
```text
[[1, 0, 0, 1], [0, 0, 1, 1], [1, 1, 0, 0]]
```
- **Explanation:** The grid is - - 0's at (0,0), (0,3), (1,2), (1,3), (2,0) and (2,1) are at a distance of 1 from 1's at (0,1), (0,2), (0,2), (2,3), (1,0) and (1,1) respectively.

##### Example 2

- **Input:**
```text
grid[][] = [[1, 0, 1], [1, 1, 0], [1, 0, 0]]
```
- **Output:**
```text
[[0, 1, 0], [0, 0, 1], [0, 1, 2]]
```
- **Explanation:** The grid is - - 0's at (0,1), (1,2), (2,1) and (2,2) are at a distance of 1, 1, 1 and 2 from 1's at (0,0), (0,2), (2,0) and (1,1) respectively.

#### Constraints

- **1.** `1 ≤ grid.size() ≤ 2001 ≤ grid[0].size() ≤ 200`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * m)
- **Expected Auxiliary Space Complexity:** O(n * m)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-19 00:56:44
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<vector<int>> nearest(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();

        // Distance matrix initialized to -1 (indicating unvisited)
        vector<vector<int>> dist(n, vector<int>(m, -1));
        queue<pair<int, int>> q;

        // Step 1: Push all '1's into the queue and set their distance to 0
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == 1) {
                    dist[i][j] = 0;
                    q.push({i, j});
                }
            }
        }

        // Direction arrays for moving up, right, down, left
        int delRow[] = {-1, 0, +1, 0};
        int delCol[] = {0, +1, 0, -1};

        // Step 2: Multi-source BFS
        while(!q.empty()) {
            int r = q.front().first;
            int c = q.front().second;
            q.pop();

            // Traverse all 4 neighbors
            for(int i = 0; i < 4; i++) {
                int nr = r + delRow[i];
                int nc = c + delCol[i];

                // If neighbor is valid and unvisited
                if(nr >= 0 && nr < n && nc >= 0 && nc < m && dist[nr][nc] == -1) {
                    dist[nr][nc] = dist[r][c] + 1;
                    q.push({nr, nc});
                }
            }
        }

        return dist;
    }
};
```

*Generated on: 8/19/2026, 12:57:13 AM*