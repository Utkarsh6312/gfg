## 01. Nth Number without Digit 9

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/nth-natural-number/1)

### Problem Description

**Task:** Given a positive integer n as string. Find n^th natural number after removing all the numbers containing the digit 9 and return it as string.

#### Examples

##### Example 1

- **Input:**
```text
n = "8"
```
- **Output:**
```text
"8"
```
- **Explanation:** After removing natural numbers which contains digit 9, first 8 numbers are 1,2,3,4,5,6,7,8 and 8^th number is 8.

##### Example 2

- **Input:**
```text
n = "9"
```
- **Output:**
```text
"10"
```
- **Explanation:** After removing natural numbers which contains digit 9, first 9 numbers are 1,2,3,4,5,6,7,8,10 and 9^th number is 10.

#### Constraints

- **1.** `1 ≤ n.length() ≤ 20`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(1)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-16 19:51:06
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    string findNth(string& n) {
        string ans = "";
        while (n != "0") {
            int rem = 0;
            string q = "";
            for (char c : n) {
                int x = rem * 10 + (c - '0');
                int d = x / 9;
                rem = x % 9;
                if (!q.empty() || d != 0) {
                    q += (char)('0' + d);
                }
            }
            ans += (char)('0' + rem);
            n = q.empty() ? "0" : q;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

*Generated on: 11/16/2026, 7:51:29 PM*