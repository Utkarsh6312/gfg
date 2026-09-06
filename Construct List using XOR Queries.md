## 01. Construct List using XOR Queries

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/construct-list-using-given-q-xor-queries/1)

### Problem Description

**Task:** There is an array that initially contains only a single value, 0.
Given a list of queries queries[][] of size q, where each query is of one of the following types:
0 x: Insert x into the array.
1 x: Replace every element a in the array with a ^ x, where ^ denotes the bitwise XOR operator.
Return the array in sorted order after performing all the queries.

#### Examples

##### Example 1

- **Input:**
```text
q = 5, queries[] = [[0, 6], [0, 3], [0, 2], [1, 4], [1, 5]]
```
- **Output:**
```text
[1, 2, 3, 7] [0] (initial value) [0, 6] (add 6 to list) [0, 6, 3] (add 3 to list) [0, 6, 3, 2] (add 2 to list) [4, 2, 7, 6] (XOR each element by 4) [1, 7, 2, 3] (XOR each element by 5) The sorted list after performing all the queries is [1, 2, 3, 7].
```

##### Example 2

- **Input:**
```text
q = 3, queries[] = [[0, 2], [1, 3], [0, 5]]
```
- **Output:**
```text
[1, 3, 5] [0] (initial value) [0, 2] (add 2 to list) [3, 1] (XOR each element by 3) [3, 1, 5] (add 5 to list) The sorted list after performing all the queries is [1, 3, 5].
```

#### Constraints

- **1.** `1 ≤ q ≤ 10⁵⁰ ≤ x ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(q*log(q))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-06 15:47:25
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> constructList(vector<vector<int>>& queries) {
        vector<int> ans;
        int current_xor = 0;

        // Process queries in reverse order
        for (int i = queries.size() - 1; i >= 0; i--) {
            if (queries[i][0] == 1) {
                // Accumulate the XOR value
                current_xor ^= queries[i][1];
            } else {
                // Apply the accumulated XOR to the inserted element
                ans.push_back(queries[i][1] ^ current_xor);
            }
        }

        // The initial 0 in the list is affected by all XOR queries
        ans.push_back(0 ^ current_xor);

        // The problem requires returning the array in sorted order
        sort(ans.begin(), ans.end());

        return ans;
    }
};
```

*Generated on: 9/6/2026, 3:47:44 PM*