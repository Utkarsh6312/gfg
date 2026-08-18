## 01. Add Binary Strings

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/add-binary-strings3805/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given two binary strings s1 and s2 consisting of only 0s and 1s. Find the resultant string after adding the two Binary Strings.Note: The input strings may contain leading zeros but the output string should not have any leading zeros.

#### Examples

##### Example 1

- **Input:**
```text
s1 = "1101", s2 = "111"
```
- **Output:**
```text
10100 1101 + 111 10100
```

##### Example 2

- **Input:**
```text
s1 = "00100", s2 = "010"
```
- **Output:**
```text
110 100 + 10 110
```

#### Constraints

- **1.** `1 ≤s1.size(), s2.size()≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-19 00:04:10
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    string addBinary(string& s1, string& s2) {
        int i = s1.length() - 1;
        int j = s2.length() - 1;
        int carry = 0;
        string result = "";

        // Pre-allocate memory to prevent dynamic reallocation overhead
        result.reserve(max(s1.length(), s2.length()) + 1);

        // Traverse both strings from right to left
        while (i >= 0 || j >= 0 || carry > 0) {
            int sum = carry;
            if (i >= 0) sum += s1[i--] - '0';
            if (j >= 0) sum += s2[j--] - '0';

            result += (sum % 2) + '0'; // Append the current bit
            carry = sum / 2;           // Calculate the new carry
        }

        // The result is currently backwards, so reverse it
        reverse(result.begin(), result.end());

        // Remove any leading zeros as per the problem requirement
        size_t start = result.find_first_not_of('0');
        if (start != string::npos) {
            return result.substr(start);
        }

        // If the string was all zeros (e.g., "00" + "000"), return "0"
        return "0";
    }
};
```

*Generated on: 8/19/2026, 12:04:20 AM*