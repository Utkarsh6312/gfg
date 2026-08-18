## 01. Max sum in the configuration

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/max-sum-in-the-configuration/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an integer array arr[]. Find the maximum value of the sum of i*arr[i] for all 0 ≤ i ≤ arr.size()-1. The only operation allowed is to rotate(clockwise or counterclockwise) the array any number of times.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [3, 1, 2, 8]
```
- **Output:**
```text
29
```
- **Explanation:** Out of all the possible configurations by rotating the elements: arr[] = [3, 1, 2, 8] here (3*0) + (1*1) + (2*2) + (8*3) = 29 is maximum.

##### Example 2

- **Input:**
```text
arr[] = [1, 2, 3]
```
- **Output:**
```text
8
```
- **Explanation:** Out of all the possible configurations by rotating the elements: arr[] = [1, 2, 3] here (1*0) + (2*1) + (3*2) = 8 is maximum.

##### Example 3

- **Input:**
```text
arr[] = [4, 13]
```
- **Output:**
```text
13
```

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁴¹ ≤ arr[i] ≤ 20`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 23:59:17
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int maxSum(vector<int>& arr) {
        long long n = arr.size();
        long long total_sum = 0;
        long long current_val = 0;

        // Step 1: Calculate the base sum of all elements 
        // and the sum of i * arr[i] for the initial configuration
        for (long long i = 0; i < n; i++) {
            total_sum += arr[i];
            current_val += i * (long long)arr[i];
        }

        long long max_val = current_val;

        // Step 2: Compute the sum for remaining configurations using the formula
        for (long long i = 1; i < n; i++) {
            current_val = current_val - total_sum + (long long)arr[i - 1] * n;
            max_val = max(max_val, current_val);
        }

        return max_val;
    }
};
```

*Generated on: 8/18/2026, 11:59:41 PM*