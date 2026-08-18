## 01. Minimum Insertions for Palindrome

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/form-a-palindrome2544/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a string s, the task is to find the minimum number of characters to be inserted to convert it to a palindrome.

#### Examples

##### Example 1

- **Input:**
```text
s = "abcd"
```
- **Output:**
```text
3
```
- **Explanation:** Here we can append 3 characters in the beginning and the resultant string will be a palindrome "dcbabcd".

##### Example 2

- **Input:**
```text
s = "aba"
```
- **Output:**
```text
0
```
- **Explanation:** Given string is already a pallindrome hence no insertions are required.

#### Constraints

- **1.** `1 ≤ s.size() ≤ 500`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-06 21:43:46
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int findMinInsertions(string &s) {
        // code here
        int n=s.size();
        vector<vector<int>> dp(n,vector<int>(n,0));
        for(int len=1;len<n;len++){
            for(int i=0;i<n-len;i++){
                int j=i+len;
                if(s[i]==s[j])dp[i][j]=dp[i+1][j-1];
                else dp[i][j]=1+min(dp[i+1][j],dp[i][j-1]);
            }
        }return dp[0][n-1];
    }
};
```

*Generated on: 8/6/2026, 9:45:30 PM*