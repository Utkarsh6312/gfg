## 01. Factorial Digits - Complete Study Guide

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/factorials-of-large-numbers2508/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an integer n, find its factorial. Return a list of integers denoting the digits that make up the factorial of n.

#### Examples

##### Example 1

- **Input:**
```text
n = 5
```
- **Output:**
```text
[1, 2, 0]
```
- **Explanation:** 5! = 1*2*3*4*5 = 120

##### Example 2

- **Input:**
```text
n = 10
```
- **Output:**
```text
[3, 6, 2, 8, 8, 0, 0]
```
- **Explanation:** 10! = 1*2*3*4*5*6*7*8*9*10 = 3628800

##### Example 3

- **Input:**
```text
n = 1
```
- **Output:**
```text
[1]
```
- **Explanation:** 1! = 1

#### Constraints

- **1.** `1 ≤ n ≤ 10³`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n^2)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-25 11:51:45
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    vector<int> factorial(int n) {
        vector<int> a;
        a.push_back(1); // Base case: 1! = 1
        
        for (int i = 2; i <= n; i++) {
            int carry = 0;
            
            // Multiply every digit in vector 'a' by 'i'
            for (int &digit : a) {
                int prod = digit * i + carry;
                digit = prod % 10;  // Store least significant digit
                carry = prod / 10;  // Pass the remaining value to carry
            }
            
            // Push any remaining carry into the vector digit by digit
            while (carry > 0) {
                a.push_back(carry % 10);
                carry /= 10;
            }
        }
        
        // Reverse to get the most significant digit first
        reverse(a.begin(), a.end());
        
        return a;
    }
};
```

*Generated on: 7/25/2026, 11:52:20 AM*