# Recent LeetCode Problem-Solving Record


&lt;!--more--&gt;
### [402. Remove K Digits](https://leetcode.com/problems/remove-k-digits)
```typescript
function removeKdigits(num: string, k: number): string {
  if (k === num.length) return &#34;0&#34;;
  let stack: string[] = [];
  let removed = 0;
  for (let i = 0; i &lt; num.length; &#43;&#43;i) {
    while (stack.length &amp;&amp; removed &lt; k &amp;&amp; num[i] &lt; stack[stack.length - 1]) {
      &#43;&#43;removed;
      stack.pop();
    }
    stack.push(num[i]);
  }
  while (removed &lt; k) {
    stack.pop();
    &#43;&#43;removed;
  }
  let flag = false;
  for (let i = 0; i &lt; stack.length; &#43;&#43;i) {
    if (stack[i] !== &#39;0&#39;) {
      flag = true;
      stack = stack.slice(i);
      break;
    }
  }
  if (!flag) return &#34;0&#34;;
  else return stack.join(&#39;&#39;);
};
```

### [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive)
```typescript
function firstMissingPositive(nums: number[]): number {
  let len = nums.length;

  for (let i = 0; i &lt; len; &#43;&#43;i) {
    while (nums[i] &gt; 0 &amp;&amp; nums[i] &lt; len &amp;&amp; i !== nums[i] - 1) {
      let index = nums[i] - 1;
      let num = nums[index];
      if (num === nums[i]) break;
      nums[index] = nums[i];
      nums[i] = num;
    }
  }
  for (let i = 0; i &lt; len; &#43;&#43;i) {
    if (nums[i] !== i &#43; 1) return i &#43; 1;
  }
  return nums[len - 1] &#43; 1;
};
```

### [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)
```typescript
function trap(height: number[]): number {
  let res = 0;
  let left = 0;
  let right = height.length - 1;
  let level = 0;
  while (left &lt; right) {
    let lower = height[left] &gt; height[right] ? height[right--] : height[left&#43;&#43;];
    level = Math.max(lower, level);
    res &#43;= level - lower;
  }
  return res;
};
```

### [1. Two Sum](https://leetcode.com/problems/two-sum)
```typescript
function twoSum(nums: number[], target: number): number[] {
  let result: number[] = [];
  let index: Map&lt;number, number[]&gt; = new Map();
  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    if (index.has(nums[i])) {
      index.set(nums[i], [...index.get(nums[i]), i]);
    } else {
      index.set(nums[i], [i]);
    }
    let n = target - nums[i];
    if (n === nums[i]) {
      if (index.get(nums[i]).length &gt;= 2) {
        result = [index.get(nums[i])[0], index.get(nums[i])[1]];
        break;
      }
    } else {
      if (index.has(n)) {
        result = [index.get(n)[0], index.get(nums[i])[0]];
        break;
      }
    }
  }
  return result;
};
```

### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)
```typescript
function reverseList(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;
    
    let prior = head;
    let ptr = prior.next;
    prior.next = null;

    while (ptr) {
      let next = ptr.next;

      ptr.next = prior;
      
      head = ptr;
      prior = ptr;
      
      ptr = next;
    }

    return head;
};
```

### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)
```typescript
function convertToTitle(columnNumber: number): string {
  let num = columnNumber.toString(26);
  let res = &#39;&#39;;

  let A = &#39;A&#39;.charCodeAt(0);
  let carry = 0;

  for (let i = num.length - 1; i &gt;= 0; --i) {
    let n = 0;
    if (num[i].charCodeAt(0) &gt;= A) n = 10 &#43; (num[i].toUpperCase()).charCodeAt(0) - A;
    else n = &#43;num[i];

    if (n === 0) {
      n = 26;
      if (carry) {
        n -= carry;
        carry = 0;
      }

      carry &#43;= 1;
      res = String.fromCharCode(A &#43; n - 1) &#43; res;
      continue;
    }

    if (carry) {
      if (n &gt;= carry) {
        n -= carry;
        carry = 0;
      } else {
        carry -= n;
        n = 0;
      }
    }
    if (n === 0) {
      if (i === 0) break;
      else {
        n = 26;
        carry &#43;= 1;
      }
    }
    res = String.fromCharCode(A &#43; n - 1) &#43; res;
  }

  return res;
};
```

### [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/description/)
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */

var maxSlidingWindow = function (nums, k) {
  let res = [];
  let window = [];
  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    if (window[0] &lt; i - k &#43; 1) window.shift();

    if (nums[i] &lt; nums[window[window.length - 1]]) window.push(i);
    else {
      while (window.length &gt; 0 &amp;&amp; nums[window[window.length - 1]] &lt;= nums[i]) window.pop();
      window.push(i);
    }

    if (i &gt;= k - 1) res.push(nums[window[0]]);
  }

  return res;
};
```

### [1472. Design Browser History](https://leetcode.com/problems/design-browser-history/description/)
```javascript
/**
 * @param {string} homepage
 */
var BrowserHistory = function (homepage) {
  this.head = { url: homepage, next: null, prior: null };
  this.current = this.head;
};

/** 
 * @param {string} url
 * @return {void}
 */
BrowserHistory.prototype.visit = function (url) {
  let next = { url: url, next: null, prior: this.current };
  this.current.next = next;
  this.current = this.current.next;
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.back = function (steps) {
  let num = 0;
  while (this.current !== this.head &amp;&amp; num &lt; steps) {
    this.current = this.current.prior;
    &#43;&#43;num;
  }
  return this.current.url;
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.forward = function (steps) {
  let num = 0;
  while (this.current.next !== null &amp;&amp; num &lt; steps) {
    this.current = this.current.next;
    &#43;&#43;num;
  }
  return this.current.url;
};

/** 
 * Your BrowserHistory object will be instantiated and called as such:
 * var obj = new BrowserHistory(homepage)
 * obj.visit(url)
 * var param_2 = obj.back(steps)
 * var param_3 = obj.forward(steps)
 */
```

### [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)
```javascript
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function (target, nums) {
  let left = 0;
  let len = nums.length;
  let res = Infinity;
  let sum = 0;

  for (let right = 0; right &lt; len; &#43;&#43;right) {
    sum &#43;= nums[right];

    while (sum &gt;= target) {
      res = Math.min(res, right - left &#43; 1);
      sum -= nums[left];
      &#43;&#43;left;
    }
  }

  return res === Infinity ? 0 : res;
};
```

### [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/description/)
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function (nums, target) {
  nums.sort((a, b) =&gt; a - b);
  let abs = Infinity;
  let res = target;

  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    let left = i &#43; 1;
    let right = nums.length - 1;

    while (left &lt; right) {
      let sum = nums[i] &#43; nums[left] &#43; nums[right];

      if (Math.abs(sum - target) &lt; abs) {
        abs = Math.abs(sum - target);
        res = sum;
      }

      if (sum === target) return res;
      else if (sum &lt; target) &#43;&#43;left;
      else --right;
    }

  }

  return res;
};
```

### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array)
```javascript
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function (nums1, m, nums2, n) {
  let i = m - 1;
  let j = n - 1;
  let k = nums1.length - 1;
  while (i &gt;= 0 || j &gt;= 0) {
    if (i &lt; 0 &amp;&amp; j &gt;= 0 || nums2[j] &gt; nums1[i]) {
      nums1[k] = nums2[j];
      --j;
    } else {
      nums1[k] = nums1[i];
      --i;
    }
    --k;
  }
};
```

### [678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/description)
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkValidString = function (s) {
  let left = [];
  let asterisk = [];
  let res = true;

  for (let i = 0; i &lt; s.length; &#43;&#43;i) {
    if (s[i] === &#39;(&#39;) left.push(i);
    else if (s[i] === &#39;*&#39;) asterisk.push(i);
    else {
      if (left.length &gt; 0) left.pop();
      else if (asterisk.length &gt; 0) asterisk.pop();
      else {
        res = false;
        break;
      }
    }
  }

  if (res === true &amp;&amp; left.length &gt; 0) {
    if (asterisk.length &gt;= left.length) {
      while (left.length){
        let l = left.pop();
        let a = asterisk.pop();
        if (a &lt;= l) {
          res = false;
          break;
        }
      }
    } else res = false;
  }

  return res;
};
```

### [1556. Thousand Separator](https://leetcode.com/problems/thousand-separator/description)
```javascript
/**
 * @param {number} n
 * @return {string}
 */
var thousandSeparator = function (n) {
  if (n &lt; 1000) return n.toString();
  let res = &#34;&#34;;
  let s = n.toString();
  let cnt = 0;

  for (let i = s.length - 1; i &gt;= 0; --i) {
    &#43;&#43;cnt;
    res = s[i] &#43; res;
    if (cnt % 3 === 0 &amp;&amp; i !== 0) res = &#39;.&#39; &#43; res;
  }

  return res;
};
```

### [39. Combination Sum](https://leetcode.com/problems/thousand-separator/description)
```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */

let set = new Set();
let res = [];
let t = 0;
let c = [];

function dfs(nums, sum) {
  if (sum === t) {
    let str = &#34;&#34;;
    for (let n of nums) str &#43;= n &#43; &#34;,&#34;;
    if (!set.has(str)) {
      res.push([...nums]);
      set.add(str);
    }
    return;
  }

  for (let i = 0; i &lt; c.length; &#43;&#43;i) {
    if (sum &#43; c[i] &gt; t) break;
    if (nums.length === 0 || c[i] &gt;= nums[nums.length - 1]) {
      nums.push(c[i]);
      sum &#43;= c[i];
      dfs(nums, sum);
      nums.pop();
      sum -= c[i];
    }
  } 
}

var combinationSum = function (candidates, target) {
  set.clear();
  res = [];
  t = target;
  c = candidates;

  candidates.sort((a, b) =&gt; a - b);

  dfs([], 0);

  return res;
};
```

### [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses)
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  let stack = [];
  let res = true;

  for (let i = 0; i &lt; s.length; &#43;&#43;i) {
    if (s[i] === &#39;(&#39;) stack.push(&#39;(&#39;);
    else if (s[i] === &#39;{&#39;) stack.push(&#39;{&#39;);
    else if (s[i] === &#39;[&#39;) stack.push(&#39;[&#39;);
    else {
      let top = stack.pop();
      if (!(top === &#39;(&#39; &amp;&amp; s[i] === &#39;)&#39; || top === &#39;{&#39; &amp;&amp; s[i] === &#39;}&#39; || top === &#39;[&#39; &amp;&amp; s[i] === &#39;]&#39;)) {
        res = false;
        break;
      }
    }
  }

  if (stack.length) res = false;

  return res;
};
```

### [415. Add Strings](https://leetcode.com/problems/add-strings)
```javascript
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
// var addStrings = function (num1, num2) {
//   return (BigInt(num1) &#43; BigInt(num2)).toString();
// };


var addStrings = function (num1, num2) {
  let a = [], b = [];

  if (num1.length &lt; num2.length) {
    let num3 = num1;
    num1 = num2;
    num2 = num3;
  }

  for (let i = 0; i &lt; num1.length; &#43;&#43;i) a.push(&#43;num1[i]);
  for (let i = 0; i &lt; num2.length; &#43;&#43;i) b.push(&#43;num2[i]);

  let x = num1.length - 1, y = num2.length - 1;
  while (y &gt;= 0) {
    a[x] &#43;= b[y];
    --x;
    --y;
  }

  x = num1.length - 1;
  while (x &gt; 0) {
    if (a[x] &gt;= 10) {
      a[x - 1] &#43;= 1;
      a[x] -= 10;
    }
    --x;
  }
  let first = a[0];

  if (first &gt;= 10) a[0] -= 10;

  if (first &gt;= 10) return 1 &#43; a.join(&#39;&#39;);
  else return a.join(&#39;&#39;);

};
```

### [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses)
```javascript
/**
 * @param {number} n
 * @return {string[]}
 */


var generateParenthesis = function (n) {
  let res = [];

  function dfs(sum, l, p, str) {
    if (sum === n) {
      res.push(str.join(&#39;&#39;));
      return;
    }

    if (l &lt; n) {
      l &#43;= 1;
      p &#43;= 1;
      str.push(&#39;(&#39;)
      dfs(sum, l, p, str);
      l -= 1;
      p -= 1;
      str.pop();
    }

    if (p &gt; 0) {
      p -= 1;
      str.push(&#39;)&#39;);
      sum &#43;= 1;
      dfs(sum, l, p, str);
      p &#43;= 1;
      str.pop();
      sum -= 1;
    }
  }

  dfs(0, 0, 0, []);

  return res;
};
```

### [75. Sort Colors](https://leetcode.com/problems/sort-colors/description/)
```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function (nums) {
  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    let flag = false;
    for (let j = 1; j &lt;= nums.length - i; &#43;&#43;j) {
      if (nums[j] &lt; nums[j - 1]) {
        flag = true;
        let tmp = nums[j];
        nums[j] = nums[j - 1];
        nums[j - 1] = tmp;
      }
    }
    if (!flag) break;
  }
};
```

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/recent-leetcode-problem-solving-record/  

