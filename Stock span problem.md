## 01. Stock span problem

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/stock-span-problem-1587115621/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** The stock span problem is a financial problem where we have a series of daily price quotes for a stock and we need to calculate the span of stock price for all days. You are given an array arr[] representing daily stock prices, the stock span for the i-th day is the number of consecutive days up to day i (including day i itself) for which the price of the stock is less than or equal to the price on day i. Return the span of stock prices for each day in the given sequence.

#### Examples

##### Example 1

- **Input:**
```text
arr[] = [100, 80, 90, 120]
```
- **Output:**
```text
[1, 1, 2, 4]
```
- **Explanation:** Traversing the given input span 100 is greater than equal to 100 and there are no more days behind it so the span is 1, 80 is greater than equal to 80 and smaller than 100 so the span is 1, 90 is greater than equal to 90 and 80 so the span is 2, 120 is greater than 90, 80 and 100 so the span is 4. So the output will be [1, 1, 2, 4].

##### Example 2

- **Input:**
```text
arr[] = [10, 4, 5, 90, 120, 80]
```
- **Output:**
```text
[1, 1, 2, 4, 5, 1]
```
- **Explanation:** Traversing the given input span 10 is greater than equal to 10 and there are no more days behind it so the span is 1, 4 is greater than equal to 4 and smaller than 10 so the span is 1, 5 is greater than equal to 4 and 5 and smaller than 10 so the span is 2, and so on. Hence the output will be [1, 1, 2, 4, 5, 1].

#### Constraints

- **1.** `1 ≤ arr.size() ≤ 10⁵¹ ≤ arr[i] ≤ 10⁵`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(n)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-04-23 11:32:23
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    vector<int> calculateSpan(vector<int>& a) {
        // code here
        int n=a.size();
        vector<int> b(n,1);
        stack<int> st;
        for(int i=n-1;i>=0;i--){
            while(!st.empty() && a[i]>a[st.top()]){
                b[st.top()]=st.top()-i;
                st.pop();
            }st.push(i);
        }
        while(!st.empty()){
            b[st.top()]=st.top()+1;
            st.pop();
        }return b;
    }
};
// 100 80 60 70 60 75 85
// 1    1  1 2  1  4  6
```

*Generated on: 4/23/2026, 11:32:43 AM*