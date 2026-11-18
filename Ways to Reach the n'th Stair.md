## 01. Ways to Reach the n'th Stair

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/count-ways-to-reach-the-nth-stair-1587115620/1)

### Problem Description

**Task:** There are n stairs, a person standing at the bottom wants to reach the top. The person can climb either 1 stair or 2 stairs at a time. Count the number of ways, the person can reach the top (order does matter). Examples:Input: n = 1

#### Examples

##### Example 1

- **Output:**
```text
5
```
- **Explanation:** There are five ways to reach 4th stair: [1, 1, 1, 1], [1, 1, 2], [2, 1, 1], [1, 2, 1] and [2, 2].

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-18 20:32:15
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int countWays(int n) {
        if (n <= 1) return 1;
        int prev2 = 1, prev1 = 1;
        for (int i = 2; i <= n; i++) {
            int curr = prev1 + prev2;
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
};
```

*Generated on: 11/18/2026, 8:32:37 PM*