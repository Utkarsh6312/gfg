## 01. Koko Eating Bananas

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/koko-eating-bananas/1)

### Problem Description

**Task:** Koko is given an array arr[], where each element represents a pile of bananas. She has exactly k hours to eat all the bananas.
Each hour, Koko can choose one pile and eat up to s bananas from it.
If the pile has atleast s bananas, she eats exactly s bananas.
If the pile has fewer than s bananas, she eats the entire pile in that hour.
Koko can only eat from one pile per hour.
Your task is to find the minimum value of s (bananas per hour) such that Koko can finish all the piles within k hours.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [5, 10, 3], k = 4
```
- **Output:**
```text
5Explanation: If Koko eats at the rate of 5 bananas per hour:First pile of 5 bananas will be finished in 1 hour. Second pile of 10 bananas will be finished in 2 hours. Third pile of 3 bananas will be finished in 1 hours.Therefore, Koko can finish all piles of bananas in 1 + 2 + 1 = 4 hours.
```

##### Example 2

- **Input:**
```text
arr[] = [5, 10, 15, 20], k = 7
```
- **Output:**
```text
10
```
- **Explanation:** If Koko eats at the rate of 10 bananas per hour, it will take 6 hours to finish all the piles.

#### Constraints

- **1.** `1 ≤ arr.size() ≤ k ≤ 10⁶¹ ≤ arr[i] ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * log(max(arr[i])))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-25 00:17:33
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int kokoEat(vector<int>& arr, int k) {
        int low = 1;
        int high = *max_element(arr.begin(), arr.end());
        int ans = high;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            long long total_hours = 0; 

            // Calculate total hours required at 'mid' speed
            for (int i = 0; i < arr.size(); i++) {
                // (arr[i] + mid - 1) / mid is equivalent to ceil(arr[i] / (double)mid) 
                // but avoids floating point precision issues.
                total_hours += (arr[i] + mid - 1) / mid;
            }

            if (total_hours <= k) {
                ans = mid;      // Record this valid speed
                high = mid - 1; // Try to find a slower valid speed
            } else {
                low = mid + 1;  // Too slow, need to eat faster
            }
        }

        return ans;
    }
};
```

*Generated on: 8/25/2026, 1:46:26 AM*