# LeetCode 66

[LeetCode 66.Plus One](https://leetcode.com/problems/plus-one/description/), is an easy problem. I just want to practice Java, it's been a long time since I wrote Java.
<!--more-->

My idea is to traverse from the end to the beginning, if the current digit is 9, then carry, if not, then add 1, and then return the result. If the last digit is 9, then we need to add a 1 at the beginning, at this time we need to create a new array, and then copy the original array.

```Java
class Solution {
    public int[] plusOne(int[] digits) {
        int end = digits.length - 1;
        int[] result = new int[end + 1];
        boolean carry = false;
        result[end] = digits[end] + 1;
        if (result[end] == 10) {
            result[end] = 0;
            carry = true;
        }
        for (int i = end - 1; i >= 0; --i) {
            result[i] = digits[i];
            if (carry) {
                result[i] += 1;
                if (result[i] == 10) {
                    result[i] = 0;
                    carry = true;
                } else {
                    carry = false;
                }
            }
        }
        if (carry) {
            int[] tmp = result;
            result = new int[end + 2];
            result[0] = 1;
            for (int i = 1; i < end + 2; ++i) {
                result[i] = tmp[i - 1];
            }
        }
        return result;
    }
}
```
