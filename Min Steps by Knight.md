## 01. Min Steps by Knight

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/steps-by-knight5927/1)

### Problem Description

**Task:** Given a square chessboard of size (n x n), the initial position and target position of Knight are given. Find out the minimum steps a Knight will take to reach the target position.Note: The initial and the target position coordinates of Knight have been given according to 1-base indexing.

#### Examples

##### Example 1

- **Input:**
```text
n = 3, knightPos[] = [3, 3], targetPos[] = [1, 2]Output: 1Explanation:Knight takes 1 step to reach from (3, 3) to (1 ,2).
```

##### Example 2

- **Input:**
```text
n = 6, knightPos[] = [4, 5],targetPos[] = [1, 1]
```
- **Output:**
```text
3 Knight takes 3 step to reach from (4, 5) to (1, 1): (4, 5) - > (5, 3) - > (3, 2) - > (1, 1).
```

#### Constraints

- **1.** `1 <= n <= 1000`
- **2.** `1 <= knightpos ≤ [x, y], targertpos[x, y] ≤ n`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(n^2)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-09 23:22:41
- **Status:** Correct
- **Marks:** 4

```cpp
#include <vector>
#include <queue>

using namespace std;

class Solution {
public:
    int minStepToReachTarget(vector<int>& knightPos, vector<int>& targetPos, int n) {
        int startX = knightPos[0] - 1;
        int startY = knightPos[1] - 1;
        int targetX = targetPos[0] - 1;
        int targetY = targetPos[1] - 1;

        if (startX == targetX && startY == targetY) {
            return 0;
        }

        vector<vector<bool>> vis(n, vector<bool>(n, false));
        queue<pair<pair<int, int>, int>> q; // Stores {{x, y}, steps}

        q.push({{startX, startY}, 0});
        vis[startX][startY] = true;

        vector<pair<int, int>> moves = {
            {2, 1}, {2, -1}, {-2, 1}, {-2, -1},
            {1, 2}, {1, -2}, {-1, 2}, {-1, -2}
        };

        while (!q.empty()) {
            auto curr = q.front();
            q.pop();

            int x = curr.first.first;
            int y = curr.first.second;
            int steps = curr.second;

            for (auto [dx, dy] : moves) {
                int nx = x + dx;
                int ny = y + dy;

                if (nx == targetX && ny == targetY) {
                    return steps + 1;
                }

                if (nx >= 0 && nx < n && ny >= 0 && ny < n && !vis[nx][ny]) {
                    vis[nx][ny] = true;
                    q.push({{nx, ny}, steps + 1});
                }
            }
        }

        return -1;
    }
};
```

*Generated on: 8/12/2026, 9:58:52 AM*