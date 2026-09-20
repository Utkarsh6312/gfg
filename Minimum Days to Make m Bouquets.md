## 01. Minimum Days to Make m Bouquets

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/minimum-days-to-make-m-bouquets/1)

### Problem Description

**Task:** In a row of flowers, each flower blooms on a specific day. Given an integer array arr[], where arr[i] denotes the day on which the flower at position i blooms.
To make a bouquet, you need to collect k adjacent flowers that have already bloomed. Each flower can be used in at most one bouquet.
Find the minimum number of days required to make m bouquets. If it is impossible to do so, return -1.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [3, 4, 2, 7, 13, 8, 5], m = 3, k = 2
```
- **Output:**
```text
8
```
- **Explanation:** We need to make 3 bouquets, each consisting of 2 adjacent flowers. - > By day 8, all flowers have bloomed except the flower at position 5 (1-indexed). - > Form the 1st bouquet using the first 2 flowers. - > Form the 2nd bouquet using the next 2 flowers. - > Form the 3rd bouquet using the last 2 flowers.

##### Example 2

- **Input:**
```text
arr[] = [5, 5, 5, 5, 10, 5, 5], m = 2, k = 3,
```
- **Output:**
```text
10
```
- **Explanation:** We need to make 2 bouquets, each consisting of 3 adjacent flowers. - > By day 5, all flowers have bloomed except the flower at position 5 (1-indexed). - > We can form the 1st bouquet using the first 3 bloomed flowers. - > It is not possible to form the 2nd bouquet now. - > By day 10, all the flowers have bloomed. - > We can then form 2 bouquets, each consisting of 3 adjacent flowers.

##### Example 3

- **Input:**
```text
m = 3, k = 2, arr[] = [1, 10, 3, 10, 2]Output: -1Explanation: We need to make 3 bouquets, each consisting of 2 flowers. - > This requires a total of 6 flowers. - > There are only 5 flowers available. - > Therefore, it is impossible to make the required bouquets.
```

#### Constraints

- **1.** `1 ≤ k ≤ arr.size() ≤ 10⁵¹ ≤ m ≤ 10⁵¹ ≤ arr[i] ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * log(max(arr[i])))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (2)

#### Solution 1 (C++)

- **Submitted:** 2026-09-20 18:23:20
- **Status:** Correct
- **Marks:** 0

```cpp
class Solution {
  private:
    bool isPossible(vector<int>& arr, int day, int m, int k) {
        int bouquets = 0;
        int bloomedCount = 0;

        for (int i = 0; i < arr.size(); i++) {
            if (arr[i] <= day) {
                bloomedCount++;
                // If we have enough adjacent flowers for a bouquet
                if (bloomedCount == k) {
                    bouquets++;
                    bloomedCount = 0; // Reset for the next bouquet
                }
            } else {
                // Sequence is broken
                bloomedCount = 0;
            }
        }

        return bouquets >= m;
    }

  public:
    int minDaysBloom(vector<int>& arr, int k, int m) {
        int n = arr.size();

        // If we need more flowers than we have, return -1
        if (1LL * m * k > n) {
            return -1;
        }

        // Find the search space range
        int low = 1, high = 1;
        for (int i = 0; i < n; i++) {
            low = min(low, arr[i]);
            high = max(high, arr[i]);
        }

        int ans = -1;

        // Binary search on the days
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isPossible(arr, mid, m, k)) {
                ans = mid;        // Potential answer
                high = mid - 1;   // Try to find an earlier day
            } else {
                low = mid + 1;    // We need more days
            }
        }

        return ans;
    }
};
```

#### Solution 2 (C++)

- **Submitted:** 2026-09-20 18:23:13
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  private:
    bool isPossible(vector<int>& arr, int day, int m, int k) {
        int bouquets = 0;
        int bloomedCount = 0;

        for (int i = 0; i < arr.size(); i++) {
            if (arr[i] <= day) {
                bloomedCount++;
                // If we have enough adjacent flowers for a bouquet
                if (bloomedCount == k) {
                    bouquets++;
                    bloomedCount = 0; // Reset for the next bouquet
                }
            } else {
                // Sequence is broken
                bloomedCount = 0;
            }
        }

        return bouquets >= m;
    }

  public:
    int minDaysBloom(vector<int>& arr, int k, int m) {
        int n = arr.size();

        // If we need more flowers than we have, return -1
        if (1LL * m * k > n) {
            return -1;
        }

        // Find the search space range
        int low = 1, high = 1;
        for (int i = 0; i < n; i++) {
            low = min(low, arr[i]);
            high = max(high, arr[i]);
        }

        int ans = -1;

        // Binary search on the days
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (isPossible(arr, mid, m, k)) {
                ans = mid;        // Potential answer
                high = mid - 1;   // Try to find an earlier day
            } else {
                low = mid + 1;    // We need more days
            }
        }

        return ans;
    }
};
```

*Generated on: 9/20/2026, 6:23:44 PM*