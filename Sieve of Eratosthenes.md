## 01. Sieve of Eratosthenes

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/sieve-of-eratosthenes5242/1)

### Problem Description

**Task:** Given a positive integer n, calculate and return all primes less than or equal to n using the Sieve of Eratosthenes algorithm.

#### Examples

##### Example 1

- **Input:**
```text
n = 10
```
- **Output:**
```text
[2, 3, 5, 7]
```
- **Explanation:** Prime numbers less than equal to 10 are 2, 3, 5 and 7.

##### Example 2

- **Input:**
```text
n = 35
```
- **Output:**
```text
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31]
```
- **Explanation:** Prime numbers less than equal to 35 are 2, 3, 5, 7, 11, 13, 17, 19, 23, 29 and 31.

#### Constraints

- **1.** `1 ≤ n ≤ 10⁴`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n*log(log(n)))
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-16 19:52:04
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> sieve(int n) {
        vector<bool> prime(n + 1, true);
        prime[0] = prime[1] = false;

        for (int p = 2; p * p <= n; p++) {
            if (prime[p]) {
                for (int i = p * p; i <= n; i += p) {
                    prime[i] = false;
                }
            }
        }

        vector<int> result;
        for (int p = 2; p <= n; p++) {
            if (prime[p]) {
                result.push_back(p);
            }
        }
        return result;
    }
};
```

*Generated on: 11/16/2026, 7:52:26 PM*