## 01. Mountain Subarray Queries

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/mountain-subarray-problem/1)

### Problem Description

**Task:** Given an array arr[] and a list of queries. For each query [l, r], find whether the subarray arr[l...r] is a mountain array. A subarray is called a mountain array if there exists an index k (l ≤ k ≤ r) such that: arr[l] ≤ arr[l + 1] ≤ ... ≤ arr[k] ≥ arr[k + 1] ≥ ... ≥ arr[r].
Elements of a Mountain subarray are first non-decreasing and then non-increasing.
A subarray that is entirely non-decreasing or entirely non-increasing is also considered a mountain.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [2, 3, 2, 4, 4, 6, 3, 2], queries[][] = [[0, 2], [1, 3]]
```
- **Output:**
```text
[true, false]
```
- **Explanation:** For query [0, 2], the subarray is [2, 3, 2]. The elements first increase and then decrease, so it forms a mountain.For query [1, 3], the subarray is [3, 2, 4]. The elements decrease and then increase, so it does not form a mountain.

##### Example 2

- **Input:**
```text
arr[] = [2, 2, 2, 2], queries[][] = [[0, 2], [1, 3]]
```
- **Output:**
```text
[true, true]
```
- **Explanation:** All subarrays of the given array are mountain.

#### Constraints

- **1.** `1 <= arr.size(), queries.size() <= 10⁵`
- **2.** `1 <= arr[i] <= 10⁶`
- **3.** `0 <= l <= r < arr.size()`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n + q)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-10-10 01:40:20
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<bool> processQueries(vector<int> &arr, vector<vector<int>> &queries) {
        int n = arr.size();
        vector<int> left(n), right(n);

        // Compute left[] array
        left[0] = 0;
        int last_inc = 0;
        for (int i = 1; i < n; i++) {
            if (arr[i] > arr[i - 1]) {
                last_inc = i;
            }
            left[i] = last_inc;
        }

        // Compute right[] array
        right[n - 1] = n - 1;
        int last_dec = n - 1;
        for (int i = n - 2; i >= 0; i--) {
            if (arr[i] > arr[i + 1]) {
                last_dec = i;
            }
            right[i] = last_dec;
        }

        // Process each query in O(1)
        vector<bool> result;
        for (const auto &q : queries) {
            int l = q[0];
            int r = q[1];

            result.push_back(right[l] >= left[r]);
        }

        return result;
    }
};
```

*Generated on: 10/10/2026, 1:40:47 AM*