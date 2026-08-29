## 01. Top k Frequent in Stream

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/top-k-numbers3425/1)

### Problem Description

**Task:** Given an array arr[] of integers and an integer k, traverse the array from left to right. After processing each element, find the k most frequent elements so far.
For each step, form an array containing these elements sorted according to the following rules:
Elements with higher frequency appear first.
If two elements have the same frequency, the smaller element appears first.
If the number of distinct elements encountered so far is less than k, include all of them.
Return a 2D array where the i-th row contains the top frequent elements after processing arr[i].

#### Examples

##### Example 1

- **Input:**
```text
k = 4, arr[] = [5, 2, 1, 3, 2]
```
- **Output:**
```text
[[5], [2, 5], [1, 2, 5], [1, 2, 3, 5], [2, 1, 3, 5]]
```
- **Explanation:** Firstly there was 5 whose frequency is max till now. So resulting sequence is [5]. Then came 2, which is smaller than 5 but their frequencies are same so resulting sequence is [2, 5]. Then came 1, which is the smallest among all the numbers arrived, so resulting sequence is [1, 2, 5]. Then came 3 , so resulting sequence is [1, 2, 3, 5].Then again 2, which has the highest frequency among all numbers, so resulting sequence is [2, 1, 3, 5].

##### Example 2

- **Input:**
```text
k = 3, arr[] = [2, 1, 2, 1, 2, 1]
```
- **Output:**
```text
[[2], [1, 2], [2, 1], [1, 2], [2, 1], [1, 2]]Explanation: As total number of distinct values never exceeds 2, you need to return only those two values. In the case where frequency of 1 gets equal with the frequency of 2, you have to keep 1 before 2 in the array.
```

#### Constraints

- **1.** `1 ≤ n ≤ 10⁴¹ ≤ k ≤ 10²^1 ≤ arr[i] ≤ 10²^`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n*k)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-29 15:31:39
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<vector<int>> kTop(int k, vector<int>& arr) {
        vector<vector<int>> ans;
        vector<int> top;
        unordered_map<int, int> freq;

        for (int x : arr) {
            // Update the frequency of the current element
            freq[x]++;

            // If x is not in our top array, add it to the end
            auto it = find(top.begin(), top.end(), x);
            if (it == top.end()) {
                top.push_back(x);
            }

            // Find the current position of x in the top array
            int pos = find(top.begin(), top.end(), x) - top.begin();

            // Bubble up x to its correct position
            // It only needs to move left since its frequency increased
            while (pos > 0) {
                int prev = top[pos - 1];
                int curr = top[pos];

                // Custom sort condition:
                // 1. Higher frequency comes first
                // 2. If frequencies are equal, smaller element comes first
                if (freq[curr] > freq[prev] || (freq[curr] == freq[prev] && curr < prev)) {
                    swap(top[pos], top[pos - 1]);
                    pos--;
                } else {
                    break;
                }
            }

            // If the top array exceeds size k, pop the last element
            if (top.size() > k) {
                top.pop_back();
            }

            // Add the current top elements to our answer
            ans.push_back(top);
        }

        return ans;
    }
};
```

*Generated on: 8/29/2026, 3:32:04 PM*