## 01. Max Occured in n Ranges

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-occured-integer4602/1)

### Problem Description

**Task:** You are given two integer arrays L[] and R[], where each L[i] and R[i] define the start and end of a range respectively. The goal is to find the integer that appears in the most number of these ranges. If multiple integers occur in the same maximum number of ranges, then return the smallest integer among them.

#### Examples

##### Example 1

- **Input:**
```text
L[] = [1, 4, 3, 1], R[] = [15, 8, 5, 4]
```
- **Output:**
```text
4
```
- **Explanation:** The given ranges are [1, 15] [4, 8] [3, 5] [1, 4]. The smallest number that is most common or appears most times in the ranges is 4.

##### Example 2

- **Input:**
```text
L[] = [1, 5, 9, 13, 21], R[] = [15, 8, 12, 20, 30]
```
- **Output:**
```text
5
```
- **Explanation:** The given ranges are [1, 15] [5, 8] [9, 12] [13, 20] [21, 30]. The smallest number that is most common or appears most times in the ranges is 5.

#### Constraints

- **1.** `1 ≤ L.size() ≤ 10⁶⁰ ≤ L[i], R[i] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n+max(R))
- **Expected Auxiliary Space Complexity:** O(max(R))

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-21 21:06:59
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int maxOccured(vector<int>& L, const vector<int>& R) {
        int n = L.size();
        int max_r = 0;

        // Find the maximum value in R[] to determine the necessary array size
        for (int i = 0; i < n; i++) {
            if (R[i] > max_r) {
                max_r = R[i];
            }
        }

        // Create a difference array. 
        // Size is max_r + 2 to safely handle the R[i] + 1 index without out-of-bounds errors.
        vector<int> diff(max_r + 2, 0);

        // Mark the start and end+1 of each range
        for (int i = 0; i < n; i++) {
            diff[L[i]]++;
            diff[R[i] + 1]--;
        }

        // Compute the prefix sum to find the actual frequencies and track the maximum
        int max_count = diff[0];
        int res = 0;

        for (int i = 1; i <= max_r; i++) {
            diff[i] += diff[i - 1]; // Build prefix sum in place

            // Strictly greater (>) ensures we keep the smallest integer in case of a tie
            if (diff[i] > max_count) {
                max_count = diff[i];
                res = i;
            }
        }

        return res;
    }
};
```

*Generated on: 8/21/2026, 9:07:32 PM*