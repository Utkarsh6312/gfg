## 01. K Closest in a Sorted Array

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/k-closest-elements3619/1)

### Problem Description

**Task:** Given a sorted array arr[] of unique integers, an integer k, and a target value x. Return exactly k elements from the array closest to x, excluding x if it exists.
An element a is closer to x than b if:
|a - x| < |b - x|, or
|a - x| = = |b - x| and a > b (i.e., prefer the larger element if tied)
Return the k closest elements in order of closeness.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [1, 3, 4, 10, 12], k = 2, x = 4
```
- **Output:**
```text
[3, 1]
```
- **Explanation:** 4 is excluded from the consideration.The closest element to 4 is 3 with a distance of 1.The next closest element is 1 with a distance of 3.

##### Example 2

- **Input:**
```text
arr[] = [10, 20, 30, 40, 50], k = 3, x = 25
```
- **Output:**
```text
[30, 20, 40]
```
- **Explanation:** First closest element to 25 is 30, since 30 > 20. Second closest element to 25 is 20. Third closest element to 25 is 40.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(log n + k)
- **Expected Auxiliary Space Complexity:** O(k)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-21 20:01:48
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> findKClosest(vector<int> arr, int k, int x) {
        int n = arr.size();
        vector<int> result;

        // Find the first element that is >= x
        int r = lower_bound(arr.begin(), arr.end(), x) - arr.begin();
        int l = r - 1;

        // If x is present in the array, skip it
        if (r < n && arr[r] == x) {
            r++;
        }

        // Find k closest elements
        while (k > 0) {
            // If both pointers are within valid array bounds
            if (l >= 0 && r < n) {
                int diff1 = x - arr[l];
                int diff2 = arr[r] - x;

                // If the left element is strictly closer, pick it
                if (diff1 < diff2) {
                    result.push_back(arr[l]);
                    l--;
                } 
                // If the right element is closer OR it's a tie (prefer larger element)
                else {
                    result.push_back(arr[r]);
                    r++;
                }
            } 
            // If only the left pointer is valid
            else if (l >= 0) {
                result.push_back(arr[l]);
                l--;
            } 
            // If only the right pointer is valid
            else if (r < n) {
                result.push_back(arr[r]);
                r++;
            }
            k--;
        }

        return result;
    }
};
```

*Generated on: 8/21/2026, 8:02:34 PM*