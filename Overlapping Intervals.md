## 01. Overlapping Intervals

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/overlapping-intervals--170633/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given an array of intervals arr[][] of size n, where arr[i] = [start_i, end_i] represents the start and end points of the ith interval, merge all overlapping intervals and return the resulting array of non-overlapping intervals.Note: Two intervals [a, b] and [c, d] such that a ≤ c, are considered overlapping if c ≤ b.

#### Examples

##### Example 1

- **Input:**
```text
arr[][] = [[1, 3], [2, 4], [6, 8], [9, 10]]
```
- **Output:**
```text
[[1, 4], [6, 8], [9, 10]]
```
- **Explanation:** In the given intervals we have only two overlapping intervals here, [1, 3] and [2, 4] which on merging will become [1, 4]. Therefore we will return [[1, 4], [6, 8], [9, 10]].

##### Example 2

- **Input:**
```text
arr[][] = [[6, 8], [1, 9], [2, 4], [4, 7]]
```
- **Output:**
```text
[[1, 9]]Explanation: In the given intervals all the intervals overlap with the interval [1, 9]. Therefore we will return [1, 9].
```

#### Constraints

- **1.** `1 ≤ n ≤ 10⁵⁰ ≤ start_i ≤ end_i ≤ 10⁶`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n log n)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (2)

#### Solution 1 (C++)

- **Submitted:** 2026-08-18 01:55:51
- **Status:** Correct
- **Marks:** 0

```cpp
class Solution {
public:
    vector<vector<int>> mergeOverlap(vector<vector<int>>& arr) {
        // Handle edge case
        if (arr.empty()) return arr;

        // Step 1: Sort the intervals based on their start times
        sort(arr.begin(), arr.end());

        // Step 2: Initialize the result vector with the first interval
        vector<vector<int>> merged;
        merged.push_back(arr[0]);

        // Step 3: Iterate through the remaining intervals
        for (int i = 1; i < arr.size(); i++) {
            // Check for overlap: current start <= last merged end
            if (arr[i][0] <= merged.back()[1]) {
                // Overlap found: update the end time
                merged.back()[1] = max(merged.back()[1], arr[i][1]);
            } else {
                // No overlap: add the new independent interval
                merged.push_back(arr[i]);
            }
        }

        return merged;
    }
};
```

#### Solution 2 (C++)

- **Submitted:** 2026-08-18 01:55:12
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    vector<vector<int>> mergeOverlap(vector<vector<int>>& a) {
        // Code here
        sort(a.begin(),a.end());
        vector<vector<int>> ans;
        auto pb = [&](const vector<int>& val){ ans.push_back(val);};
        pb(a[0]);
        for(int i=1 ;i<a.size();i++){
            if(a[i][0]<=ans.back()[1]){
                ans.back()[1]=max(ans.back()[1],a[i][1]);
            }else{
                pb(a[i]);
            }
        }return ans;
    }
};
```

*Generated on: 8/18/2026, 1:56:37 AM*