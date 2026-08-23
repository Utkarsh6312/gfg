## 01. Product Pair

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/equal-to-product3836/1)

### Problem Description

**Task:** Given an integer array arr[] and an integer target, determine whether there exists a pair of elements in the array whose product is equal to target.
Return true if such a pair exists; otherwise, return false.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [10, 20, 9, 40], target = 400
```
- **Output:**
```text
true
```
- **Explanation:** As 10 * 40 = 400, the answer is true.

##### Example 2

- **Input:**
```text
arr[] = [-10, 20, 9, -40], target = 30
```
- **Output:**
```text
false
```
- **Explanation:** No pair exists with product 30.

##### Example 3

- **Input:**
```text
arr[] = [-10, 0, 9, -40], target = 0
```
- **Output:**
```text
true
```
- **Explanation:** As -10 * 0 = 0, the answer is true.

#### Constraints

- **1.** `2 ≤ arr.size ≤ 10⁵-10⁸ ≤ arr[i] ≤ 10⁸-10¹⁸ ≤ target ≤ 10¹⁸`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (2)

#### Solution 1 (C++)

- **Submitted:** 2026-08-23 18:31:15
- **Status:** Correct
- **Marks:** 0

```cpp
class Solution {
public:
    bool isProduct(vector<int>& arr, long long target) {
        if (target == 0) {
            for (int x : arr) {
                if (x == 0) return true;
            }
            return false;
        }

        sort(arr.begin(), arr.end());
        int n = arr.size();

        for (int i = 0; i < n; i++) {
            if (arr[i] == 0) continue;

            if (target % arr[i] == 0) {
                long long req = target / arr[i];

                // If the required pair is a different number, a standard binary search works
                if (req != arr[i]) {
                    if (binary_search(arr.begin(), arr.end(), req)) {
                        return true;
                    }
                } 
                // If the required pair is the same number, check adjacent elements
                else {
                    if ((i > 0 && arr[i-1] == req) || (i + 1 < n && arr[i+1] == req)) {
                        return true;
                    }
                }
            }
        }

        return false;
    }
};
```

#### Solution 2 (C++)

- **Submitted:** 2026-08-23 18:31:03
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    bool isProduct(vector<int>& arr, long long target) {
        // Special case: if target is 0, we just need at least one 0 in the array
        if (target == 0) {
            for (int x : arr) {
                if (x == 0) return true;
            }
            return false;
        }

        unordered_set<long long> seen;
        for (long long x : arr) {
            // Avoid division by zero, and check if the required multiplier exists
            if (x != 0 && target % x == 0 && seen.count(target / x)) {
                return true;
            }
            seen.insert(x);
        }

        return false;
    }
};
```

*Generated on: 8/23/2026, 6:36:30 PM*