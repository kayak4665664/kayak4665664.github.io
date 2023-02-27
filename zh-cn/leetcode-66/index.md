# LeetCode 66

[LeetCode 66.Plus One](https://leetcode.com/problems/plus-one/description/)，一道简单的题。主要是想练习一下Java，好长时间没写Java了。
<!--more-->

我的思路是从后往前遍历，如果当前位是9，那么就进位，如果不是9，那么就加1，然后返回结果。如果最后一位是9，那么就需要在最前面加一个1，这个时候就需要新建一个数组，然后把原来的数组复制过去。

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

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/leetcode-66/  

