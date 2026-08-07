## 01. Maximum Index

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-index3307/1?page=1&category=Arrays,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an array, arr[] of non-negative integers. The task is to return the maximum of j - i (i <= j) subjected to the constraint of arr[i] <= arr[j].

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [34, 8, 10, 3, 2, 80, 30, 33, 1]Output: 6Explanation: In the given array arr[1] < arr[7] satisfying the required condition (arr[i] <= arr[j]) thus giving the maximum difference of j - i which is 7-1 = 6.
```

##### Example 2

- **Input:**
```text
arr[] = [18, 17]Output: 0Explanation: We can either take i and j as 0 and 0 or we cantake 1 and 1 both give the same result 0.
```

##### Example 3

- **Input:**
```text
arr[] = [10, 10, 10, 10]Output: 3Explanation: Since all elements are equal, any pair of indices will satisfy the condition arr[i] <= arr[j]. The maximum difference is between j = 3 and i = 0, resulting in j - i = 3.
```

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁶⁰ ≤ arr[i] ≤ 10⁹`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-04-23 12:31:56
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int maxIndexDiff(vector<int>& a) {
        // code here
        int n=a.size(); 
        vector<int> mina(n),maxa(n);
        mina[0]=a[0];
        maxa[n-1]=a[n-1];
        int i;
        for(i=1;i<n;i++){
                mina[i]=min(a[i],mina[i-1]);
                maxa[n-i-1]=max(a[n-i-1],maxa[n-i]);
        } 
        int j=0,ans=0;i=0;
        while(i<n && j<n){
            if(mina[i]<=maxa[j]){
                ans=max(ans,j-i);
                j++;
            }else i++;
        }return ans;
    }
};
```

*Generated on: 4/23/2026, 12:32:09 PM*