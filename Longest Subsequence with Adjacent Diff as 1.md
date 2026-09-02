## 01. Longest Subsequence with Adjacent Diff as 1

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/longest-sub-sequence-such-that-difference-between-adjacents-is-one2558/1)

### Problem Description

**Task:** Given an array arr[] with n elements. find the longest subsequence such that the absolute difference between adjacent elements is one.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [10, 9, 4, 5, 4, 8, 6]
```
- **Output:**
```text
3
```
- **Explanation:** Longest subsequences with difference 1 are [10, 9, 8], [4, 5, 4] and [4, 5, 6].

##### Example 2

- **Input:**
```text
arr[] = [1, 2, 3, 2, 3, 7, 2, 1]
```
- **Output:**
```text
7Explanation: Longest subsequences with difference 1 is [1, 2, 3, 2, 3, 2, 1].
```

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-03 02:12:15
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int longestSubseq(vector<int>& arr) {
        if (arr.empty()) return 0;

        // Find the maximum element to size our DP array
        int max_ele = 0;
        for (int num : arr) {
            max_ele = max(max_ele, num);
        }

        // dp[i] will store the maximum length of a valid subsequence ending with the value 'i'
        // We size it to max_ele + 2 to avoid out-of-bounds when checking num + 1
        vector<int> dp(max_ele + 2, 0);
        int max_len = 1;

        for (int num : arr) {
            // The current number can extend a subsequence ending in (num - 1) or (num + 1)
            int len = 0;
            if (num > 0) {
                len = max(len, dp[num - 1]);
            }
            len = max(len, dp[num + 1]);

            // Update the dp array for the current number
            dp[num] = len + 1;

            // Keep track of the overall maximum length found so far
            max_len = max(max_len, dp[num]);
        }

        return max_len;
    }
};
```

*Generated on: 9/3/2026, 2:12:36 AM*