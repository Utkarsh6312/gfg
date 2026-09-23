## 01. Easy Java Solution using Comparator Sorting in TC : O(nlogn)

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/farthest-smaller-right/1)

### Problem Description

**Task:** You are given an array arr[]. For each element at index i (0-based indexing), find the farthest index j to the right (i.e., j > i) such that arr[j] < arr[i]. If no such index exists for a given position, return -1 for that index. Return the resulting array of answers.Examples:Input: arr[] = [2, 5, 1, 3, 2]Output: [2, 4, -1, 4, -1]Explanation: arr[0] = 2: Farthest smaller element to the right is arr[2] = 1.arr[1] = 5: Farthest smaller element to the right is arr[4] = 2.arr[2] = 1: No smaller element to the right → -1.arr[3] = 3: Farthest smaller element to the right is arr[4] = 2.arr[4] = 2: No elements to the right → -1.Input: arr[] = [2, 3, 5, 4, 1] Output: [4, 4, 4, 4, -1]Explanation: arr[4] is the farthest smallest element to the right for arr[0], arr[1], arr[2] and arr[3].

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n log n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-23 12:22:02
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> farMin(vector<int>& arr) {
        int n = arr.size();
        vector<int> ans(n, -1);
        vector<int> suffixMin(n);

        // Precompute suffix minimums
        suffixMin[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffixMin[i] = min(arr[i], suffixMin[i + 1]);
        }

        // For each element, binary search for the farthest smaller element to the right
        for (int i = 0; i < n; i++) {
            int low = i + 1, high = n - 1;
            int farthestIndex = -1;

            while (low <= high) {
                int mid = low + (high - low) / 2;

                // If suffixMin[mid] < arr[i], a valid smaller element exists at or to the right of mid
                if (suffixMin[mid] < arr[i]) {
                    farthestIndex = mid;
                    low = mid + 1; // Try to find a farther index to the right
                } else {
                    high = mid - 1; // Look in the left half
                }
            }

            ans[i] = farthestIndex;
        }

        return ans;
    }
};
```

*Generated on: 9/23/2026, 12:22:32 PM*