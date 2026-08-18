## 01. Transform Array In-Place

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/rearrange-an-array-with-o1-extra-space3142/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an integer array arr[] of size n, where each element lies in the range [0, n-1], transform the array such that every element at index i becomes:arr[i] = arr[arr[i]].
The transformation must be performed in-place, meaning the same array should store both the original and updated values without using another array.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [1, 0]
```
- **Output:**
```text
[0, 1]
```
- **Explanation:** The original array is [1, 0]. At index 0, arr[0] = 1, so the new value becomes arr[1] = 0. At index 1, arr[1] = 0, so the new value becomes arr[0] = 1. Thus, the transformed array becomes [0, 1].

##### Example 2

- **Input:**
```text
arr[] = [4, 0, 2, 1, 3]
```
- **Output:**
```text
[3, 4, 2, 0, 1]
```
- **Explanation:** The original array is [4, 0, 2, 1, 3]. Each element is replaced by the value at index arr[i] in the original array. So the new values become 3, 4, 2, 0, 1 respectively, and the transformed array becomes [3, 4, 2, 0, 1].

#### Constraints

- **1.** `1 ≤ n ≤ 4*10⁴⁰ ≤ arr[i] < n`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-09 22:25:11
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    void arrange(vector<int>& arr) {
        int n = arr.size();
        
        for (int i = 0; i < n; i++) {
            arr[i] += (arr[arr[i]] % n) * n;
        }
        
        for (int i = 0; i < n; i++) {
            arr[i] /= n;
        }
    }
};
```

*Generated on: 8/9/2026, 10:25:43 PM*