## 01. Rod Cutting

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/rod-cutting0840/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a rod of length n inches and an array price[], where price[i] denotes the value of a piece of length i. Your task is to determine the maximum value obtainable by cutting up the rod and selling the pieces.

> **Note:** n = size of price, and price[] is 1-indexed array.

#### Examples

##### Example 1

- **Input:**
```text
price[] = [1, 5, 8, 9, 10, 17, 17, 20]Output: 22Explanation: The maximum obtainable value is 22 by cutting in two pieces of lengths 2 and 6, i.e., 5 + 17 = 22.
```

##### Example 2

- **Input:**
```text
price[] = [3, 5, 8, 9, 10, 17, 17, 20]Output: 24Explanation: The maximum obtainable value is 24 by cutting the rod into 8 pieces of length 1, i.e, 8*price[1] = 8*3 = 24.
```

##### Example 3

- **Input:**
```text
price[] = [3]Output: 3Explanation: There is only 1 way to pick a piece of length 1.
```

#### Constraints

- **1.** `1 ≤ price.size() ≤ 10³¹ ≤ price[i] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-13 17:32:23
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int cutRod(vector<int> &p) {
        // code here
        int n=p.size();
        vector<int> dp(n+1,0);
        for(int i =1;i<=n;i++){
            int m=INT_MIN;
            for(int j=1;j<=i;j++){
                m=max(m,p[j-1]+dp[i-j]);
            }dp[i]=m;
        }return dp[n];
    }
};
```

*Generated on: 7/13/2026, 5:32:48 PM*