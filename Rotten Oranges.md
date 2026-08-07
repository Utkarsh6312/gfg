## 01. Rotten Oranges

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/rotten-oranges2536/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a matrix mat[][], where each cell in the matrix can have values 0, 1 or 2 which has the following meaning:0 : Empty cell1 : Cell have fresh oranges2 : Cell have rotten oranges
Your task is to determine the minimum time required so that all the oranges become rotten. A rotten orange at index (i, j) can rot other fresh orange at indexes (i-1, j), (i+1, j), (i, j-1), (i, j+1) (up, down, left and right) in a unit time.

> **Note:** If it is impossible to rot every orange then simply return -1.

#### Examples

##### Example 1

- **Input:**
```text
mat[][] = [[2, 1, 0, 2, 1], [1, 0, 1, 2, 1], [1, 0, 0, 2, 1]]
```
- **Output:**
```text
2
```
- **Explanation:** Oranges at positions (0,0), (0,3), (1,3), and (2,3) will rot adjacent fresh oranges in successive time frames.All fresh oranges become rotten after 2 units of time.

##### Example 2

- **Input:**
```text
mat[][] = [[2, 1, 0, 2, 1], [0, 0, 1, 2, 1], [1, 0, 0, 2, 1]]
```
- **Output:**
```text
-1
```
- **Explanation:** Oranges at positions (0,0), (0,3), (1,3), and (2,3) rot some fresh oranges,but the fresh orange at (2,0) can never be reached, so not all oranges can rot.

#### Constraints

- **1.** `1 ≤ mat.size() ≤ 5001 ≤ mat[0].size() ≤ 500mat[i][j] = {0, 1, 2}`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * m)
- **Expected Auxiliary Space Complexity:** O(n * m)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-13 17:05:10
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int orangesRot(vector<vector<int>>& mat) {
        int n = mat.size();
        int m = mat[0].size();
        
        // Queue to store coordinates of rotten oranges: {row, col}
        queue<pair<int, int>> q;
        int fresh_count = 0;
        
        // Step 1: Initialize the queue with all initial rotten oranges
        // and count the total number of fresh oranges.
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (mat[i][j] == 2) {
                    q.push({i, j});
                } else if (mat[i][j] == 1) {
                    fresh_count++;
                }
            }
        }
        
        // If there are no fresh oranges to begin with, 0 time is needed.
        if (fresh_count == 0) return 0;
        
        int time = 0;
        
        // Direction vectors for moving Up, Down, Left, and Right
        int dRow[] = {-1, 1, 0, 0};
        int dCol[] = {0, 0, -1, 1};
        
        // Step 2: Process the grid layer by layer (BFS)
        while (!q.empty()) {
            int size = q.size();
            bool rotted_any_this_turn = false;
            
            // Process all oranges at the current time step
            for (int i = 0; i < size; i++) {
                auto [r, c] = q.front();
                q.pop();
                
                // Check all 4 adjacent directions
                for (int d = 0; d < 4; d++) {
                    int nRow = r + dRow[d];
                    int nCol = c + dCol[d];
                    
                    // Check bounds and if the neighbor is a fresh orange
                    if (nRow >= 0 && nRow < n && nCol >= 0 && nCol < m && mat[nRow][nCol] == 1) {
                        mat[nRow][nCol] = 2; // Turn it rotten
                        q.push({nRow, nCol}); // Add to queue for the next time frame
                        fresh_count--;
                        rotted_any_this_turn = true;
                    }
                }
            }
            
            // Only increment time if we actually spread the rot to new oranges
            if (rotted_any_this_turn) {
                time++;
            }
        }
        
        // Step 3: If fresh oranges still remain, return -1
        return (fresh_count == 0) ? time : -1;
    }
};
```

*Generated on: 7/13/2026, 5:05:59 PM*