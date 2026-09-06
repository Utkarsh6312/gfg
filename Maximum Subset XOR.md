## 01. Maximum Subset XOR

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-subset-xor/1)

### Problem Description

**Task:** Given an array arr[], choose any subset of elements (possibly all elements) such that the XOR of the chosen elements is maximized.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [2, 4, 5]Output: 7Explanation: The subset {2, 5} has the maximum XOR value.
```

##### Example 2

- **Input:**
```text
arr[] = [9, 8, 5]Output: 13Explanation: The subset {8, 5} has the maximum XOR value.
```

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * log(max(arr[i])))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-06 16:04:10
- **Status:** Correct
- **Marks:** 8

```cpp
class Solution {
public:
    int maxSubsetXOR(vector<int>& arr) {
        // Array to store the basis for each bit position (0 to 31)
        int basis[32] = {0};

        // Build the linear basis
        for (int x : arr) {
            for (int i = 31; i >= 0; i--) {
                // If the i-th bit is set in x
                if ((x >> i) & 1) {
                    if (!basis[i]) {
                        basis[i] = x;
                        break;
                    }
                    // If basis[i] is already occupied, XOR x with basis[i] to cancel the bit
                    x ^= basis[i];
                }
            }
        }

        // Find the maximum XOR subset using the basis
        int ans = 0;
        for (int i = 31; i >= 0; i--) {
            if ((ans ^ basis[i]) > ans) {
                ans ^= basis[i];
            }
        }

        return ans;
    }
};
```

*Generated on: 9/6/2026, 4:04:28 PM*