## 01. Fraction Pairs with Sum 1

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/fraction-pairs-with-sum-1/1)

### Problem Description

**Task:** Given a list of fractions, represented as two lists numerator and denominator, the task is to determine the count of pairs of fractions whose sum equals 1.
Example 1:

#### Examples

##### Example 1

- **Input:**
```text
numerator[] = [1, 2, 2, 8], denominator[] = [2, 4, 6, 12]Output: 2
```
- **Explanation:** Fractions 1/2 and 2/4 sum to 1. Similarly fractions 2/6 and 8/12 sum to 1. So there are 2 pairs of fractions which sum to 1.

##### Example 2

- **Input:**
```text
numerator[] = [3, 1, 12, 81, 2], denominator[] = [9, 10, 18, 90, 5]Output: 2
```
- **Explanation:** Fractions 3/9 and 12/18 sum to 1. Similarly fractions 1/10 and 81/90 sum to 1. So there are 2 pairs of fractions which sum to 1.

#### Constraints

- **1.** `1 ≤ numerator.size() ≤ 10⁵¹ ≤ numerator[i] ≤ denominator[i] ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n log n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-29 15:37:52
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int countFractions(vector<int>& numerator, vector<int>& denominator) {
        // Map to store the frequency of each simplified fraction
        map<pair<int, int>, int> fractionCount;
        int totalPairs = 0;

        int n = numerator.size();
        for (int i = 0; i < n; i++) {
            // Find GCD to reduce the fraction
            int g = std::gcd(numerator[i], denominator[i]);
            int num = numerator[i] / g;
            int den = denominator[i] / g;

            // The required fraction to make the sum 1
            int req_num = den - num;
            int req_den = den;

            // If the required complement exists, add its frequency to our answer
            if (fractionCount.find({req_num, req_den}) != fractionCount.end()) {
                totalPairs += fractionCount[{req_num, req_den}];
            }

            // Add the current simplified fraction to the map
            fractionCount[{num, den}]++;
        }

        return totalPairs;
    }
};
```

*Generated on: 8/29/2026, 3:38:31 PM*