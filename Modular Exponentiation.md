## 01. Modular Exponentiation

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/modular-exponentiation-for-large-numbers5537/1)

### Problem Description

**Task:** Given three integers x, n, and M, compute (x^n) % M, i.e., the remainder when x raised to the power n is divided by M.

#### Examples

##### Example 1

- **Input:**
```text
x = 3, n = 2, M = 4
```
- **Output:**
```text
1
```
- **Explanation:** 3² % 4 = 9 % 4 = 1.

##### Example 2

- **Input:**
```text
x = 2, n = 6, M = 10
```
- **Output:**
```text
4
```
- **Explanation:** 2⁶ % 10 = 64 % 10 = 4.

#### Constraints

- **1.** `1 ≤ x, n, M ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(log n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-16 19:48:09
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int powMod(int a, int n, int m) {
        // code here
        long long int ans = 1;
        long long x=(long long)(a);
        x = x % m;
        while (n > 0) {
             if (n & 1) {
                 ans = (ans * x) % m;
             }
             x = (x * x) % m;
             n >>= 1;
         }
        return (int)ans;
        
    }
};
```

*Generated on: 11/16/2026, 7:48:35 PM*