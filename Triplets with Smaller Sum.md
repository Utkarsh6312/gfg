## 01. Triplets with Smaller Sum

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/count-triplets-with-sum-smaller-than-x5549/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an array arr[] of distinct integers and a value sum, find the count of triplets (i, j, k), having (i < j < k) with the sum of (arr[i] + arr[j] + arr[k]) smaller than the given value sum.

#### Examples

##### Example 1

- **Input:**
```text
sum = 2, arr[] = [-2, 0, 1, 3]
```
- **Output:**
```text
2
```
- **Explanation:** Triplets with sum less than 2 are (-2, 0, 1) and (-2, 0, 3).

##### Example 2

- **Input:**
```text
sum = 12, arr[] = [5, 1, 3, 4, 7]
```
- **Output:**
```text
4
```
- **Explanation:** Triplets with sum less than 12 are (1, 3, 4), (5, 1, 3), (1, 3, 7) and (5, 1, 4).

#### Constraints

- **1.** `1 ≤ sum ≤ 10⁵³ ≤ arr.size() ≤ 10³-10³ ≤ arr[i] ≤ 10³`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 23:50:37
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int countTriplets(int sum, vector<int>& a) {
        // Sort the array first
        sort(a.begin(), a.end());
        int n = a.size();
        int count = 0;

        // Fix the first element
        for (int i = 0; i < n - 2; i++) {
            int left = i + 1;
            int right = n - 1;

            // Two-pointer approach for the remaining elements
            while (left < right) {
                if (a[i] + a[left] + a[right] < sum) {
                    // All elements from left+1 to right will form a valid 
                    // triplet with a[i] and a[left]
                    count += (right - left);
                    left++;
                } else {
                    // Sum is too large, reduce the right pointer
                    right--;
                }
            }
        }

        return count;
    }
};
```

*Generated on: 8/18/2026, 11:52:17 PM*