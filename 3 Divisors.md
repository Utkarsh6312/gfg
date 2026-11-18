## 01. 3 Divisors

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/3-divisors3942/1)

### Problem Description

**Task:** You are given an integer array queries[], where each element represents a query value n. For every n in the array, determine how many numbers less than or equal to n have exactly 3 divisors.

#### Examples

##### Example 1

- **Input:**
```text
queries[] = [6]
```
- **Output:**
```text
[1]
```
- **Explanation:** There is only one number 4 which has exactly three divisors 1, 2 and 4 and less than equal to 6.

##### Example 2

- **Input:**
```text
query[] = [3, 10]
```
- **Output:**
```text
[0, 2]
```
- **Explanation:** For query[0], the answer is 0. For query[1], there are two numbers 4 and 9 having exactly 3 divisors.

#### Constraints

- **1.** `1 ≤ q ≤ 10³, where q is number of elements in the queries.1 ≤ queries[i] ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(q*n*log(log(n)))
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-18 17:04:41
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> threeDivisors(vector<int> query) {
        int q = query.size();
        long long max_val = 0;
        for (int i = 0; i < q; i++) {
            if (query[i] > max_val) {
                max_val = query[i];
            }
        }

        int limit = sqrt(max_val);
        vector<bool> is_prime(limit + 1, true);
        if (limit >= 0) is_prime[0] = false;
        if (limit >= 1) is_prime[1] = false;

        for (int p = 2; p * p <= limit; p++) {
            if (is_prime[p]) {
                for (int i = p * p; i <= limit; i += p) {
                    is_prime[i] = false;
                }
            }
        }

        vector<long long> prime_squares;
        for (long long p = 2; p <= limit; p++) {
            if (is_prime[p]) {
                prime_squares.push_back(p * p);
            }
        }

        vector<int> ans;
        for (int i = 0; i < q; i++) {
            long long n = query[i];
            int count = upper_bound(prime_squares.begin(), prime_squares.end(), n) - prime_squares.begin();
            ans.push_back(count);
        }

        return ans;
    }
};
```

*Generated on: 11/18/2026, 5:05:06 PM*