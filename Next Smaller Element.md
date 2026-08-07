## 01. Next Smaller Element

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/immediate-smaller-element1142/1?page=1&category=Arrays,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** You are given an integer array arr[ ]. For every element in the array, your task is to determine its Next Smaller Element (NSE).
The Next Smaller Element (NSE) of an element x is the first element that appears to the right of x in the array and is strictly smaller than x.
If no such element exists, assign -1 as the NSE for that position.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [4, 8, 5, 2, 25]
```
- **Output:**
```text
[2, 5, 2, -1, -1]
```
- **Explanation:** The first element smaller than 4 having index > 0 is 2.The first element smaller than 8 having index > 1 is 5.The first element smaller than 5 having index > 2 is 2.There are no elements smaller than 4 having index > 3.There are no elements smaller than 4 having index > 4.

##### Example 2

- **Input:**
```text
arr[] = [13, 7, 6, 12]
```
- **Output:**
```text
[7, 6, -1, -1]
```
- **Explanation:** The first element smaller than 13 having index > 0 is 7.The first element smaller than 7 having index > 1 is 6.There are no elements smaller than 6 having index > 2.There are no elements smaller than 12 having index > 3.

##### Example 3

- **Input:**
```text
arr[] = [4, 1]
```
- **Output:**
```text
[1, -1]
```
- **Explanation:** 4 will be updated to 1 and 1 will be updated to -1.

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁵¹ ≤ arr[i] ≤ 10⁵`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-04-23 12:03:13
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    vector<int> nextSmallerEle(vector<int>& a) {
        //  code here
        int n=a.size();
        vector<int> c;
        vector<int> b(n,-1);
        for(int i=n-1;i>=0;i--){
            for(int j=c.size()-1;j>=0;j--){
                if(a[i]>c[j]){
                    b[i]=c[j];break;
                };
            }
            while(!c.empty() && c.back()>=a[i])c.pop_back();
            c.push_back(a[i]);
            
        }return b;
        
    }
}; 

// 2 25
```

*Generated on: 4/23/2026, 12:03:48 PM*