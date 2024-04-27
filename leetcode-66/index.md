# LeetCode 66

[LeetCode 66.Plus One](https://leetcode.com/problems/plus-one/description/), is an easy problem. I just want to practice Java, it&#39;s been a long time since I wrote Java.
&lt;!--more--&gt;

My idea is to traverse from the end to the beginning, if the current digit is 9, then carry, if not, then add 1, and then return the result. If the last digit is 9, then we need to add a 1 at the beginning, at this time we need to create a new array, and then copy the original array.

```Java
class Solution {
    public int[] plusOne(int[] digits) {
        int end = digits.length - 1;
        int[] result = new int[end &#43; 1];
        boolean carry = false;
        result[end] = digits[end] &#43; 1;
        if (result[end] == 10) {
            result[end] = 0;
            carry = true;
        }
        for (int i = end - 1; i &gt;= 0; --i) {
            result[i] = digits[i];
            if (carry) {
                result[i] &#43;= 1;
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
            result = new int[end &#43; 2];
            result[0] = 1;
            for (int i = 1; i &lt; end &#43; 2; &#43;&#43;i) {
                result[i] = tmp[i - 1];
            }
        }
        return result;
    }
}
```

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/leetcode-66/  

