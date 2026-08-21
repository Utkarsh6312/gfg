## 01. O(n) / O(n)

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/sorted-subsequence-of-size-3/1)

### Problem Description

**Task:** Given an array arr[], find any subsequence of three elements such that, arr[i] < arr[j] < arr[k] and (i < j < k).
If such a subsequence exists, return the three elements as an array. Otherwise, return an empty array.
The driver code will print 1 if the returned subsequence is valid and present in the array.
The driver code will print 0 if no such subsequence exists.
If the returned subsequence does not satisfy the required format or conditions, the output will be -1.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [12, 11, 10, 5, 6, 2, 30]
```
- **Output:**
```text
1
```
- **Explanation:** As 5 < 6 < 30, and they appear in the same sequence in the array. So output is 1.

##### Example 2

- **Input:**
```text
arr[] = [1, 2, 3, 4]
```
- **Output:**
```text
1
```
- **Explanation:** As the array is sorted, for every i, j, k, where i < j < k, arr[i] < arr[j] < arr[k].So output is 1.

##### Example 3

- **Input:**
```text
arr[] = [4, 3, 2, 1]
```
- **Output:**
```text
0
```
- **Explanation:** No such Subsequence exist, so empty array is returned (the driver code automatically prints 0 in this case).

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁵¹ ≤ arr[i] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-21 21:30:15
- **Status:** Correct
- **Marks:** 4

```cpp
#include <vector>
#include <climits>

using namespace std;

class Solution {
public:
    vector<int> find3Numbers(vector<int>& arr) {
        int n = arr.size();
        if (n < 3) return {}; // A subsequence of 3 requires at least 3 elements

        int num1 = INT_MAX; 
        int num2 = INT_MAX; 
        int num1_for_num2 = INT_MAX; 

        for (int x : arr) {
            if (x <= num1) {
                // Update the smallest element found so far
                num1 = x; 
            } else if (x <= num2) {
                // x is strictly greater than num1 but smaller than or equal to num2
                // Lock in num2 and store the num1 that precedes it
                num2 = x; 
                num1_for_num2 = num1; 
            } else {
                // x is strictly greater than num2 (which is strictly greater than num1_for_num2)
                // We have successfully found our triplet!
                return {num1_for_num2, num2, x};
            }
        }

        // If the loop finishes without returning, no such subsequence exists
        return {};
    }
};
```

*Generated on: 8/21/2026, 9:30:45 PM*