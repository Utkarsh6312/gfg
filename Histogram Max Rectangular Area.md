## 01. Histogram Max Rectangular Area

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1?page=1&category=Arrays,Stack,Queue,Map,set&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** You are given a histogram represented by an array arr[ ], where each element of the array denotes the height of the bars in the histogram. All bars have the same width of 1 unit.
Your task is to find the largest rectangular area possible in the given histogram, where the rectangle can be formed using a number of contiguous bars.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [60, 20, 50, 40, 10, 50, 60]
```
- **Output:**
```text
100
```
- **Explanation:** We get the maximum by picking bars highlighted above in green (50, and 60). The area is computed (smallest height) * (no. of the picked bars) = 50 * 2 = 100.

##### Example 2

- **Input:**
```text
arr[] = [3, 5, 1, 7, 5, 9]
```
- **Output:**
```text
15
```
- **Explanation:** We get the maximum by picking bars 7, 5 and 9. The area is computed (smallest height) * (no. of the picked bars) = 5 * 3 = 15.

##### Example 3

- **Input:**
```text
arr[] = [3]
```
- **Output:**
```text
3
```
- **Explanation:** In this example the largest area would be 3 of height 3 and width 1.

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁵⁰ ≤ arr[i] ≤ 10⁴`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-04-28 19:39:16
- **Status:** Correct
- **Marks:** 8

```cpp
class Solution {
  public:
    int getMaxArea(vector<int> &arr) {
        stack<int> st; // Stack indexes store karega (increasing order of heights)
        int n = arr.size();
        
        int left, right, height, ele;
        int ans = 0;
        
        for(int i = 0; i < n; i++) {
            // Agar current element chota hai stack ke top se, 
            // toh matlab stack wala bar 'right side' se limit ho gaya hai.
            while(!st.empty() && arr[st.top()] >= arr[i]) {
                ele = st.top(); // Yeh woh bar hai jiska area hum calculate kar rahe hain
                st.pop();
                
                height = arr[ele];
                
                // Right boundary: current index 'i' iska right limit hai
                right = i;
                
                // Left boundary: stack mein pop hone ke baad jo top hai, woh left limit hai
                // Agar stack khali hai, toh matlab peeche koi chota bar nahi hai (-1)
                left = st.empty() ? -1 : st.top();
                
                // Formula: Height * (Right Index - Left Index - 1)
                ans = max(ans, height * (right - left - 1));
            }
            // Current index ko stack mein daal do
            st.push(i);
        }
        
        // Agar loop khatam hone ke baad stack mein kuch bars bach gaye hain,
        // iska matlab inka koi 'right smaller' element nahi mila (limit n tak jayegi)
        while(!st.empty()) {
            ele = st.top();
            st.pop();
            
            height = arr[ele];
            
            // Inka right boundary histogram ka end (n) hoga
            right = n;
            left = st.empty() ? -1 : st.top();
                
            ans = max(ans, height * (right - left - 1));
        }
        
        return ans;
    }
};
```

*Generated on: 4/28/2026, 7:39:38 PM*