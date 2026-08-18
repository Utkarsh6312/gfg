## 01. Consecutive 1's not allowed

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/consecutive-1s-not-allowed1912/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a positive integer n, count all possible distinct binary strings of length n such that there are no consecutive 1’s.

#### Examples

##### Example 1

- **Input:**
```text
n = 3
```
- **Output:**
```text
5
```
- **Explanation:** 5 strings are ("000", "001", "010", "100", "101").

##### Example 2

- **Input:**
```text
n = 2
```
- **Output:**
```text
3
```
- **Explanation:** 3 strings are ("00", "01", "10").

##### Example 3

- **Input:**
```text
n = 1
```
- **Output:**
```text
2
```

#### Constraints

- **1.** `1 ≤ n ≤ 44`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-06 21:56:28
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int countStrings(int n) {
        // code here
        if(n==1)return 2;
        if(n==2)return 3;
        int prev1=3,prev2=2;
        int curr=0;
        for(int i=3;i<=n;i++){
            curr= prev1+prev2;
            prev2=prev1;
            prev1=curr;
        }return prev1;
    }
};
```

*Generated on: 8/6/2026, 9:56:46 PM*