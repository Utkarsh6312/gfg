## 01. Largest Prime Factor

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/largest-prime-factor2601/1)

### Problem Description

**Task:** Given a number n, your task is to find the largest prime factor of n.

#### Examples

##### Example 1

- **Input:**
```text
n = 5
```
- **Output:**
```text
5
```
- **Explanation:** The prime factorization of 5 is just 5. Therefore, the largest prime factor is 5.

##### Example 2

- **Input:**
```text
n = 24
```
- **Output:**
```text
3
```
- **Explanation:** The prime factorization of 24 is 2³×3. Among the prime factors (2, 3), the largest is 3.

##### Example 3

- **Input:**
```text
n = 13195
```
- **Output:**
```text
29
```
- **Explanation:** The prime factorization of 13195 is 5×7×13×29. The largest prime factor is 29.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(sqrt(n))
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-10-17 15:40:29
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
  public:
    int largestPrimeFactor(int n) {
        int largest=-1;
        while (n%2==0){
            largest=2;
            n/=2;
        }
        for(int i=3;i*i<=n;i+=2){
            while(!(n%i)){
                largest=i;
                n/=i;
            }
        }
        if(n>2)largest=n;
        return largest;
    }
};
```

*Generated on: 10/17/2026, 3:40:55 PM*