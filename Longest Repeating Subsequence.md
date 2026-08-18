## 01. Longest Repeating Subsequence

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/longest-repeating-subsequence2004/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given string str, find the length of the longest repeating subsequence such that it can be found twice in the given string.
The two identified subsequences A and B can use the same ith character from string s if and only if that ith character has different indices in A and B. For example, A = "xax" and B = "xax" then the index of the first "x" must be different in the original string for A and B.

#### Examples

##### Example 1

- **Input:**
```text
s = "axxzxy"
```
- **Output:**
```text
2
```
- **Explanation:** The given array with indexes looks like a x x z x y 0 1 2 3 4 5 The longest subsequence is "xx". It appears twice as explained below. subsequence A x x 0 1 < -- index of subsequence A ------ 1 2 < -- index of s subsequence B x x 0 1 < -- index of subsequence B ------ 2 4 < -- index of s We are able to use character 'x' (at index 2 in s) in both subsequences as it appears on index 1 in subsequence A and index 0 in subsequence B.

##### Example 2

- **Input:**
```text
s = "axxxy"
```
- **Output:**
```text
2
```
- **Explanation:** The given array with indexes looks like a x x x y 0 1 2 3 4 The longest subsequence is "xx". It appears twice as explained below. subsequence A x x 0 1 < -- index of subsequence A ------ 1 2 < -- index of s subsequence B x x 0 1 < -- index of subsequence B ------ 2 3 < -- index of s We are able to use character 'x' (at index 2 in s) in both subsequencesas it appears on index 1 in subsequence A and index 0 in subsequence B.

#### Constraints

- **1.** `1 <= s.size() <= 10³`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(n^2)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-06 21:14:21
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int longestRepSubseq(string &s) {
        int n = s.length();
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

        // Fill the DP table similar to Longest Common Subsequence
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                // Characters match AND their indices in the original string are different
                if (s[i - 1] == s[j - 1] && i != j) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[n][n];
    }
};
```

*Generated on: 8/6/2026, 9:15:25 PM*