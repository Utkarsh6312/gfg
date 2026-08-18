## 01. Swap Pairs Make Sum Equal

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/swapping-pairs-make-sum-equal4142/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given two arrays of integers a[] and b[], the task is to check if a pair of values (one value from each array) exists such that swapping the elements of the pair will make the sum of two arrays equal.

#### Examples

##### Example 1

- **Input:**
```text
a[] = [4, 1, 2, 1, 1, 2], b[] = [3, 6, 3, 3]
```
- **Output:**
```text
true
```
- **Explanation:** Sum of elements in a[] = 11, Sum of elements in b[] = 15, To get same sum from both arrays, we can swap following values: 1 from a[] and 3 from b[]

##### Example 2

- **Input:**
```text
a[] = [5, 7, 4, 6], b[] = [1, 2, 3, 8]
```
- **Output:**
```text
true
```
- **Explanation:** We can swap 6 from array a[] and 2 from array b[]

##### Example 3

- **Input:**
```text
a[] = [3, 3], b[] = [6, 5, 6, 6]
```
- **Output:**
```text
false
```

#### Constraints

- **1.** `1 ≤ a.size() ≤ 10⁶¹ ≤ b.size() ≤ 10⁶¹ ≤ a[i] ≤ 10³¹ ≤ b[i] ≤ 10³`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n * log n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 02:09:37
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    bool findSwapValues(vector<int>& a, vector<int>& b) {
        // code here
        int sa=accumulate(a.begin(),a.end(),0);
        int sb=accumulate(b.begin(),b.end(),0);
        int d=sa-sb;
        if(d&1)return 0;
        sort(a.begin(),a.end());
        int t=d/2;
        for(auto y:b){
            long long x=y+t;
            if(binary_search(a.begin(),a.end(),(int)x))return 1;
        }return 0;
    }
};
```

*Generated on: 8/18/2026, 2:10:04 AM*