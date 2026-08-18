## 01. Largest number in K swaps

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/largest-number-in-k-swaps-1587115620/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a number k and string s of digits denoting a positive integer, build the largest number possible by performing swap operations on the digits of s at most k times.

#### Examples

##### Example 1

- **Input:**
```text
s = "1234567", k = 4
```
- **Output:**
```text
7654321
```
- **Explanation:** Three swaps can make the input 1234567 to 7654321, swapping 1 with 7, 2 with 6 and finally 3 with 5.

##### Example 2

- **Input:**
```text
s = "3435335", k = 3
```
- **Output:**
```text
5543333
```
- **Explanation:** Three swaps can make the input 3435335 to 5543333, swapping 3 with 5, 4 with 5 and finally 3 with 4.

##### Example 3

- **Input:**
```text
s = "1034", k = 2
```
- **Output:**
```text
4301Explanation: Two swaps can make the input 1034 to 4301, swapping 1 with 4 and finally 0 with 3.
```

#### Constraints

- **1.** `1 ≤ s.size() ≤ 151 ≤ k ≤ 7`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O((n ^ 2) ^ k)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 21:17:51
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
private:
    void solve(string str, int k, string &max_str, int idx) {
        // Base case: If no swaps left or we reached the end of the string
        if (k == 0 || idx == str.length()) {
            return;
        }

        // Find the maximum digit in the remaining string
        char max_char = str[idx];
        for (int i = idx + 1; i < str.length(); i++) {
            if (str[i] > max_char) {
                max_char = str[i];
            }
        }

        // If the maximum digit is greater than the current digit, it will consume a swap
        if (max_char != str[idx]) {
            // Iterate from the end to handle multiple occurrences of the max digit
            for (int i = str.length() - 1; i > idx; i--) {
                if (str[i] == max_char) {
                    swap(str[idx], str[i]);

                    // Update global maximum string
                    if (str > max_str) {
                        max_str = str;
                    }

                    // Recur for the next index with k decremented
                    solve(str, k - 1, max_str, idx + 1);

                    // Backtrack
                    swap(str[idx], str[i]);
                }
            }
        } else {
            // If the current position is already the largest, no swap is needed.
            // Move to the next index without reducing k.
            solve(str, k, max_str, idx + 1);
        }
    }

public:
    // Function to find the largest number after k swaps.
    string findMaximumNum(string s, int k) {
        string max_str = s;
        solve(s, k, max_str, 0);
        return max_str;
    }
};
```

*Generated on: 8/18/2026, 9:47:58 PM*