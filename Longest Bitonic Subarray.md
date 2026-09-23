## 01. Longest Bitonic Subarray

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-length-bitonic-subarray5730/1)

### Problem Description

**Task:** Given an array arr[] containing positive integers, return the maximum length of the bitonic subarray.
A subarray arr[i...j] is considered bitonic if its elements first monotonically increase, and then monotonically decrease. Formally, there exists an index k (where i <= k <= j) such that:
arr[i] <= arr[i+1] <= . . . <= arr[k]
arr[k] >= arr[k+1] >= . . . >= arr[j]

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [12, 4, 78, 90, 45, 23]
```
- **Output:**
```text
5
```
- **Explanation:** The longest bitonic subarray is [4, 78, 90, 45, 23], it starts increasing at 4, peaks at 90, and decreases to 23, giving length of 5.

##### Example 2

- **Input:**
```text
arr[] = [10, 20, 30, 40]
```
- **Output:**
```text
4
```
- **Explanation:** The array [10, 20, 30, 40] is striclty increasing with no decreasing part, so longest bitonic subarray is the entire array itself, giving a length of 4.

##### Example 3

- **Input:**
```text
arr[] = [10, 10, 10, 10]
```
- **Output:**
```text
4
```

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁶¹ ≤ arr[i] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-23 12:32:38
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int bitonic(vector<int>& arr) {
        int n = arr.size();
        if (n == 0) return 0;

        std::vector<int> inc(n, 1);
        std::vector<int> dec(n, 1);

        // Step 1: Compute non-decreasing lengths from left to right
        for (int i = 1; i < n; i++) {
            if (arr[i] >= arr[i - 1]) {
                inc[i] = inc[i - 1] + 1;
            }
        }

        // Step 2: Compute non-increasing lengths from right to left
        for (int i = n - 2; i >= 0; i--) {
            if (arr[i] >= arr[i + 1]) {
                dec[i] = dec[i + 1] + 1;
            }
        }

        // Step 3: Combine left-side and right-side subsegments
        int max_len = 0;
        for (int i = 0; i < n; i++) {
            max_len = std::max(max_len, inc[i] + dec[i] - 1);
        }

        return max_len;
    }
};
```

*Generated on: 9/23/2026, 12:33:06 PM*