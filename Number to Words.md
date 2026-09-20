## 01. Number to Words

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/number-to-words0335/1)

### Problem Description

**Task:** Write a function to convert a given number n into words. We need to break down the number into International Number System, i.e., smaller groups of three digits (hundreds, tens, and ones), and convert each group into words.Examples :Input: n = 0

#### Examples

##### Example 1

- **Output:**
```text
"One Hundred Twenty Three"
```

##### Example 2

- **Input:**
```text
n = 10245
```
- **Output:**
```text
"Ten Thousand Two Hundred Forty Five"Input: n = 2147483647Output: "Two Billion One Hundred Forty Seven Million Four Hundred Eighty Three Thousand Six Hundred Forty Seven"
```

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(1)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-09-20 20:41:34
- **Status:** Correct
- **Marks:** 4

```cpp
#include <string>
#include <vector>

class Solution {
private:
    const std::vector<std::string> ones = {
        "", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine",
        "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen",
        "Seventeen", "Eighteen", "Nineteen"
    };

    const std::vector<std::string> tens = {
        "", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"
    };

    const std::vector<std::string> thousands = {
        "", "Thousand", "Million", "Billion"
    };

    // Helper function to process groups of three digits (0 to 999)
    std::string solveThreeDigits(int n) {
        std::string res = "";

        if (n >= 100) {
            res += ones[n / 100] + " Hundred";
            n %= 100;
            if (n > 0) res += " ";
        }

        if (n >= 20) {
            res += tens[n / 10];
            if (n % 10 > 0) {
                res += " " + ones[n % 10];
            }
        } else if (n > 0) {
            res += ones[n];
        }

        return res;
    }

public:
    std::string convertToWords(int n) {
        if (n == 0) return "Zero";

        std::string result = "";
        int i = 0;

        while (n > 0) {
            if (n % 1000 != 0) {
                std::string group = solveThreeDigits(n % 1000);
                if (!thousands[i].empty()) {
                    group += " " + thousands[i];
                }
                if (!result.empty()) {
                    result = group + " " + result;
                } else {
                    result = group;
                }
            }
            n /= 1000;
            i++;
        }

        return result;
    }
};
```

*Generated on: 9/20/2026, 8:42:02 PM*