## 01. Distinct Pairs with Diff K

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/count-distinct-pairs-with-difference-k1233/1)

### Problem Description

**Task:** Given an integer array of size n and a non-negative integer k, count all distinct pairs with a difference equal to k, i.e., arr[ i ] - arr[ j ] = k.

#### Examples

##### Example 1

- **Input:**
```text
arr = [1, 5, 4, 1, 2], k = 0
```
- **Output:**
```text
1
```
- **Explanation:** There is only one pair (1, 1) whose difference equal to 0.

##### Example 2

- **Input:**
```text
arr = [1, 5, 3], k = 2
```
- **Output:**
```text
2
```
- **Explanation:** There are two pairs (5, 3) and (1, 3) whose difference equal to 2.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-29 15:40:23
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    int countPairs(vector<int>& arr, int k) {
        unordered_map<int, int> freq;
        int count = 0;

        // Store the frequency of each element
        for (int num : arr) {
            freq[num]++;
        }

        // Iterate through the unique elements in the map
        for (auto it : freq) {
            int num = it.first;

            // Edge case: If k is 0, we just need at least two identical elements
            if (k == 0) {
                if (it.second > 1) {
                    count++;
                }
            } 
            // Normal case: Check if (num + k) exists in the map
            else {
                if (freq.find(num + k) != freq.end()) {
                    count++;
                }
            }
        }

        return count;
    }
};
```

*Generated on: 8/29/2026, 3:40:44 PM*