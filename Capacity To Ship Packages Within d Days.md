## 01. Capacity To Ship Packages Within d Days

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/capacity-to-ship-packages-within-d-days/1)

### Problem Description

**Task:** Given arr[] of weights, find the minimum boat capacity to ship all weights within d days.
The items are loaded in the same order as their appearance.
The total weight should not exceed the computed capacity on any day.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [1, 2, 1], d = 2
```
- **Output:**
```text
3
```
- **Explanation:** We can ship with boat capacity 3 in 2 days. Day 1- 1, 2 Day 2- 1

##### Example 2

- **Input:**
```text
arr[] = [9, 8, 10], d = 3
```
- **Output:**
```text
10
```
- **Explanation:** We can ship with boat capacity 10 in 3 days. Day 1- 9 Day 2- 8 Day 3- 10

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * log(sum(arr)))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-20 20:37:51
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    bool isp(vector<int>& a, int x, int d) {
        int c = 1, s = 0;
        for (int i = 0; i < a.size(); i++) {
            if (s + a[i] <= x) {
                s += a[i];
            } else {
                c++;
                s = a[i];
            }
        }
        return c <= d;
    }

    int leastWeightCapacity(vector<int>& a, int d) {
        int l = *max_element(a.begin(), a.end());
        int h = accumulate(a.begin(), a.end(), 0);
        int ans = h;

        while (l <= h) {
            int mid = l + (h - l) / 2;
            if (isp(a, mid, d)) {
                ans = mid;
                h = mid - 1; // Try to find a smaller valid capacity
            } else {
                l = mid + 1; // Capacity too small, increase it
            }
        }
        return ans;
    }
};
```

*Generated on: 9/20/2026, 8:38:19 PM*