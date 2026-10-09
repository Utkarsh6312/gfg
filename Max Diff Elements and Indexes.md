## 01. Max Diff Elements and Indexes

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-value-of-difference-of-a-pair-of-elements-and-their-index/1)

### Problem Description

**Task:** Given an array arr[] of positive integers. Find maximum value of |arr[i] – arr[j]| + |i – j|, (0 <= i, j <= n – 1)

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [1, 2, 3, 1]
```
- **Output:**
```text
4
```
- **Explanation:** Choosing i = 0 and j = 2, will result in |1-3|+|0-2| = 4, which is the maximum possible value.

##### Example 2

- **Input:**
```text
arr[] = [1, 1, 1]
```
- **Output:**
```text
2
```
- **Explanation:** Choosing i = 0 and j = 2, will result in |1-1|+|0-2| = 2, which is the maximum possible value.

#### Constraints

- **1.** `1 <= arr.size() <= 10⁶`
- **2.** `0 <= arr[i] <= 10⁵`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-10-10 00:54:37
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int maxValue(vector<int>& arr) {
        int n = arr.size();
        
        int max1 = INT_MIN, min1 = INT_MAX;
        int max2 = INT_MIN, min2 = INT_MAX;
        
        for (int i = 0; i < n; i++) {
            // Case 1: arr[i] + i
            max1 = max(max1, arr[i] + i);
            min1 = min(min1, arr[i] + i);
            
            // Case 2: arr[i] - i
            max2 = max(max2, arr[i] - i);
            min2 = min(min2, arr[i] - i);
        }
        
        return max(max1 - min1, max2 - min2);
    }
};
```

*Generated on: 10/10/2026, 12:55:05 AM*