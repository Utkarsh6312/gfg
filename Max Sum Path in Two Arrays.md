## 01. Max Sum Path in Two Arrays

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/max-sum-path-in-two-arrays/1)

### Problem Description

**Task:** Given two sorted arrays of distinct integers in increasing order a[] and b[], which may have some common elements, find the maximum sum of a path from the beginning of any array to the end of any array. You may switch from one array to the other only at common elements.

> **Note:** When switching, count the common element only once.

#### Examples

##### Example 1

- **Input:**
```text
a[] = [2, 3, 7, 10, 12], b[] = [1, 5, 7, 8]
```
- **Output:**
```text
35
```
- **Explanation:** The path will be (1 + 5 + 7 + 10 + 12) = 35, where 1 and 5 come from arr2 and then 7 is common so we switch to arr1 and add 10 and 12.

##### Example 2

- **Input:**
```text
a[] = [1, 2, 3], b[] = [3, 4, 5]
```
- **Output:**
```text
15
```
- **Explanation:** The path will be (1 + 2 + 3 + 4 + 5) = 15.

#### Constraints

- **1.** `1 ≤ a.size(), b.size() ≤ 10⁴¹ ≤ a[i], b[i] ≤ 10⁵`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n + m)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-22 22:02:47
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int maxPathSum(vector<int>& a, vector<int>& b) {
        int i = 0, j = 0;
        int n = a.size(), m = b.size();

        long long sum1 = 0, sum2 = 0;
        long long result = 0;

        while (i < n && j < m) {
            if (a[i] < b[j]) {
                sum1 += a[i++];
            } else if (a[i] > b[j]) {
                sum2 += b[j++];
            } else {
                // Common element found
                result += max(sum1, sum2) + a[i];
                sum1 = 0;
                sum2 = 0;
                i++;
                j++;
            }
        }

        // Add remaining elements of array 'a'
        while (i < n) {
            sum1 += a[i++];
        }

        // Add remaining elements of array 'b'
        while (j < m) {
            sum2 += b[j++];
        }

        // Add the maximum of the remaining sums
        result += max(sum1, sum2);

        return result;
    }
};
```

*Generated on: 8/22/2026, 10:03:12 PM*