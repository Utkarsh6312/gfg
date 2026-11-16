## 01. Jumping Numbers

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/jumping-numbers3805/1)

### Problem Description

**Task:** Given a positive number, n, find the largest Jumping Number that is smaller than or equal to x.
A number is called a Jumping Number if all adjacent digits in it differ by only 1.
All single-digit numbers are considered as Jumping Numbers.
For example, 7, 898, 7 and 4343456 are Jumping numbers but 796, 677, and 89098 are not.

#### Examples

##### Example 1

- **Input:**
```text
n = 10
```
- **Output:**
```text
10
```
- **Explanation:** 10 is the largest Jumping Number possible for x = 10.

##### Example 2

- **Input:**
```text
n = 50
```
- **Output:**
```text
45
```
- **Explanation:** 45 is the largest Jumping Number possible for X = 50.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-16 19:49:46
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    long long jumpingNums(long long X) {
        // code here
        if (X <= 9) return X;
            long long ans = 0;
            for (int i = 1; i <= 9 && i <= X; i++) {
                queue<long long> q;
                q.push(i);
                while (!q.empty()) {
                    long long num = q.front();
                    q.pop();
                    if (num <= X) {
                        ans = max(ans, num);
                        int last_digit = num % 10;
                        if (last_digit == 0) {
                            q.push(num * 10 + 1);
                        } else if (last_digit == 9) {
                            q.push(num * 10 + 8);
                        } else {
                            q.push(num * 10 + (last_digit - 1));
                            q.push(num * 10 + (last_digit + 1));
                        }
                    }
                }
            }
        return ans;
    }
};
```

*Generated on: 11/16/2026, 7:50:11 PM*