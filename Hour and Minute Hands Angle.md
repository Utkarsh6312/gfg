## 01. Hour and Minute Hands Angle

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/angle-between-hour-and-minute-hand0545/1)

### Problem Description

**Task:** Given a string s representing time in 24-hour format "HH:MM", compute the smallest angle in degrees between the hour and minute hands of an analog clock.

#### Examples

##### Example 1

- **Input:**
```text
s = "06:00"
```
- **Output:**
```text
180.000
```
- **Explanation:** When the time is 06:00, the angle between the hour and minute hands of the clock is 180.000 degrees.

##### Example 2

- **Input:**
```text
s = "03:15"
```
- **Output:**
```text
7.500
```
- **Explanation:** When the time is 03:15, the angle between the hour and minute hands of the clock is 7.500 degrees.

#### Constraints

- **1.** `s.size() = 500 ≤ HH ≤ 2300 ≤ MM ≤ 59`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(1)
- **Expected Auxiliary Space Complexity:** O(1)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-11-18 16:56:50
- **Status:** Correct
- **Marks:** 4

```cpp
class Solution {
public:
    double getAngle(string& s) {
        int h = stoi(s.substr(0, 2));
        int m = stoi(s.substr(3, 2));

        h = h % 12;

        double hour_angle = 0.5 * (h * 60 + m);
        double minute_angle = 6.0 * m;

        double angle = abs(hour_angle - minute_angle);
        angle = min(360.0 - angle, angle);

        return angle;
    }
};
```

*Generated on: 11/18/2026, 4:57:12 PM*