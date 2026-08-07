## 01. Longest substring with distinct characters

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/longest-distinct-characters-in-string5848/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** You are given a string s. You have to find the length of the longest substring with all distinct characters.

#### Examples

##### Example 1

- **Input:**
```text
s = "geeksforgeeks"
```
- **Output:**
```text
7
```
- **Explanation:** "eksforg" is the longest substring with all distinct characters.

##### Example 2

- **Input:**
```text
s = "aaa"
```
- **Output:**
```text
1
```
- **Explanation:** "a" is the longest substring with all distinct characters.

##### Example 3

- **Input:**
```text
s = "abcdefabcbb"
```
- **Output:**
```text
6
```
- **Explanation:** The longest substring with all distinct characters is "abcdef", which has a length of 6.

#### Constraints

- **1.** `1 ≤ s.size() ≤ 10⁵^s consists of lowercase english letters.`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-07-13 19:16:37
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int longestUniqueSubstr(string &s) {
        vector<int> f(26, 0);   // Frequency track karne ke liye
        vector<int> li(26, -1); // Last index track karne ke liye
        
        int si = 0; // Window ka start index
        int n = s.size();
        int m = 0;  // Max length (0 se start karenge)
        
        for (int i = 0; i < n; i++) {
            int c = s[i] - 'a';
            f[c]++;
            
            // Agar character repeat hua, toh window ko tab tak shrink karo
            // jab tak ki wo duplicate character window se bahar na nikal jaye
            while (f[c] > 1) {
                f[s[si] - 'a']--; // Purane characters ki frequency hatao
                si++;             // Start pointer ko aage badhao
            }
            
            // Pichla index update karo
            li[c] = i;
            
            // BUG FIX: Har ek valid window par max length update honi chahiye
            m = max(m, i - si + 1); 
        }
        
        return m;
    }
};
```

*Generated on: 7/13/2026, 7:17:08 PM*