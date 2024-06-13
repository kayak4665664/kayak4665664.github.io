# Recent LeetCode Top Interview 150 Problem-Solving Record

[LeetCode Top Interview 150](https://leetcode.com/studyplan/top-interview-150)
&lt;!--more--&gt;

### [9. Palindrome Number](https://leetcode.com/problems/palindrome-number)

```typescript
function isPalindrome(x: number): boolean {
  let str = x.toString();
  let len = str.length;
  for (let i = 0; i &lt; len / 2; &#43;&#43;i) {
    if (str[i] !== str[len - i - 1]) return false;
  }
  return true;
};
```
### [69. Sqrt(x)](https://leetcode.com/problems/sqrtx)

```typescript
function mySqrt(x: number): number {
  for (let i = 1; i &lt;= x; &#43;&#43;i) {
    if (i * i &gt; x) return i - 1;
    else if (i * i === x) return i;
    else continue;
  }
  return x;
};
```
### [169. Majority Element](https://leetcode.com/problems/majority-element)
```typescript
function majorityElement(nums: number[]): number {
  let res = 0, cnt = 0;
  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    if (cnt === 0) {
      res = nums[i];
      &#43;&#43;cnt;
    } else if (nums[i] === res) &#43;&#43;cnt
    else --cnt;
  }
  return res;
};
```

&lt;!-- ! --&gt;
### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome)
```typescript
function isPalindrome(s: string): boolean {
  let str = &#34;&#34;;
  let a = &#34;a&#34;.charCodeAt(0), z = &#34;z&#34;.charCodeAt(0);
  let A = &#34;A&#34;.charCodeAt(0), Z = &#34;Z&#34;.charCodeAt(0);
  let _0 = &#34;0&#34;.charCodeAt(0), _9 = &#34;9&#34;.charCodeAt(0);
  for (let c of s) {
    let code = c.charCodeAt(0);
    if (code &gt;= a &amp;&amp; code &lt;= z || code &gt;= _0 &amp;&amp; code &lt;= _9) str &#43;= c;
    else if (code &gt;= A &amp;&amp; code &lt;= Z) str &#43;= c.toLowerCase();
  }
  let left = 0, right = str.length - 1;
  while (left &lt;= right) {
    if (str[left] !== str[right]) return false;
    &#43;&#43;left;
    --right;
  }
  return true;
};
```

&lt;!-- ! --&gt;
### [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum)
```typescript
function minSubArrayLen(target: number, nums: number[]): number {
  let left = 0, sum = 0, len = nums.length, res = Infinity;
  for (let right = 0; right &lt; len; &#43;&#43;right) {
    sum &#43;= nums[right];
    while (sum &gt;= target) {
      res = Math.min(res, right - left &#43; 1);
      sum -= nums[left];
      left &#43;= 1;
    }
  }
  if (res === Infinity) return 0;
  else return res;
};
```

### [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku)
```typescript
function isValidSudoku(board: string[][]): boolean {
  let rows: Map&lt;string, number&gt;[] = [], cols: Map&lt;string, number&gt;[] = [], boxes: Map&lt;string, number&gt;[] = [];
  for (let i = 0; i &lt; 9; i&#43;&#43;) {
    rows[i] = new Map();
    cols[i] = new Map();
    boxes[i] = new Map();
  }

  for (let i = 0; i &lt; 9; &#43;&#43;i) {
    for (let j = 0; j &lt; 9; &#43;&#43;j) {
      let s = board[i][j];
      if (s === &#34;.&#34;) continue;
      if (rows[i].has(s)) return false;
      else rows[i].set(s, 1);
      if (cols[j].has(s)) return false;
      else cols[j].set(s, 1);
      let k = Math.trunc(i / 3) * 3 &#43; Math.trunc(j / 3);
      if (boxes[k].has(s)) return false;
      else boxes[k].set(s, 1);
    }
  }

  return true;
};
```
### [205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings)
```typescript
function isIsomorphic(s: string, t: string): boolean {
  let ms = new Map(), mt = new Map();
  for (let i = 0; i &lt; s.length; &#43;&#43;i) {
    if (ms.has(s[i])) {
      if (ms.get(s[i]) !== t[i]) return false;
    } else ms.set(s[i], t[i]);

    if (mt.has(t[i])) {
      if (mt.get(t[i]) !== s[i]) return false;
    } else mt.set(t[i], s[i]);
  }
  return true;
};
```

### [228. Summary Ranges](https://leetcode.com/problems/summary-ranges)
```typescript
function summaryRanges(nums: number[]): string[] {
  let res = [];
  let left = 0, right = 0, len = nums.length;
  while (left &lt; len &amp;&amp; right &lt; len) {
    &#43;&#43;right;
    if (right &gt;= len || nums[right] - nums[left] &gt; right - left) {
      if (right - 1 === left) res.push(nums[left].toString());
      else res.push(nums[left].toString() &#43; &#34;-&gt;&#34; &#43; nums[right - 1].toString());
      left = right;
    }
  }

  return res;
};
```

### [71. Simplify Path](https://leetcode.com/problems/simplify-path)
```typescript
function simplifyPath(path: string): string {
  let dirs = [&#34;&#34;];
  let dir = &#34;&#34;;
  let flag = false;
  for (let c of path) {
    if (flag === false) {
      if (c !== &#34;/&#34;) {
        dir = c;
        flag = true;
      }
    } else {
      if (c !== &#34;/&#34;) dir &#43;= c;
      else {
        if (dir === &#34;..&#34;) {
          if (dirs.length &gt; 1) dirs.pop();
        }
        else if (dir !== &#34;.&#34;) dirs.push(dir);
        flag = false;
      }
    }
  }
  if (flag === true) {
    if (dir === &#34;..&#34;) {
      if (dirs.length &gt; 1) dirs.pop();
    }
    else if (dir !== &#34;.&#34;) dirs.push(dir);
    flag = false;
  }
  if (dirs.length === 1) return &#34;/&#34;;
  else return dirs.join(&#34;/&#34;)
};
```

&lt;!-- ! --&gt;
### [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii)
```typescript
function reverseBetween(head: ListNode | null, left: number, right: number): ListNode | null {
  if (left === right || head === null) return head;

  let nums = [], cnt = 0, ptr = head;

  while (true) {
    &#43;&#43;cnt;
    if (cnt &gt;= left &amp;&amp; cnt &lt;= right) nums.push(ptr.val);
    if (ptr.next) ptr = ptr.next;
    else break;
  }

  ptr = head;
  cnt = 0;
  let len = nums.length;

  while (true) {
    &#43;&#43;cnt;
    if (cnt &gt;= left &amp;&amp; cnt &lt;= right) ptr.val = nums[--len];
    if (ptr.next) ptr = ptr.next;
    else break;
  }

  return head;
};
```

### [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)
```typescript
// class TreeNode {
//   val: number
//   left: TreeNode | null
//   right: TreeNode | null
//   constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
//     this.val = (val === undefined ? 0 : val)
//     this.left = (left === undefined ? null : left)
//     this.right = (right === undefined ? null : right)
//   }
// }

let res = 0;


function dfs(node: TreeNode | null, depth: number): void {
  if (node === null) return;
  &#43;&#43;depth;
  if (depth &gt; res) res = depth;
  dfs(node.left, depth);
  dfs(node.right, depth);
}

function maxDepth(root: TreeNode | null): number {
  res = 0;
  dfs(root, 0);
  return res;
};
```

### [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree)
```typescript
// class TreeNode {
//   val: number
//   left: TreeNode | null
//   right: TreeNode | null
//   constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
//     this.val = (val === undefined ? 0 : val)
//     this.left = (left === undefined ? null : left)
//     this.right = (right === undefined ? null : right)
//   }
// }

function averageOfLevels(root: TreeNode | null): number[] {
  let queue = [];
  let res = [], sum = 0, cnt = 0;

  queue.push(root);

  while (queue.length &gt; 0) {
    sum = 0;
    cnt = 0;
    let tmp = [];
    for (let node of queue) {
      sum &#43;= node!.val;
      &#43;&#43;cnt;

      if (node!.left !== null) tmp.push(node!.left);
      if (node!.right !== null) tmp.push(node!.right);
    }
    res.push(sum / cnt);
    queue = tmp;
  }
  return res;
};
```

### [530. Minimum Absolute Difference in BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst)
```typescript
// class TreeNode {
//   val: number
//   left: TreeNode | null
//   right: TreeNode | null
//   constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
//     this.val = (val === undefined ? 0 : val)
//     this.left = (left === undefined ? null : left)
//     this.right = (right === undefined ? null : right)
//   }
// }

let vals: number[] = [];

function dfs(node: TreeNode | null): void {
  if (node === null) return;
  vals.push(node.val);
  dfs(node.left);
  dfs(node.right);
}

function getMinimumDifference(root: TreeNode | null): number {
  vals = [];
  dfs(root);
  vals.sort((a, b) =&gt; a - b);

  let len = vals.length;
  let res = Infinity;
  for (let i = 1; i &lt; len; &#43;&#43;i) {
    let d = vals[i] - vals[i - 1];
    if (d &lt; res) res = d;
  }
  return res;
};

```

### [200. Number of Islands](https://leetcode.com/problems/number-of-islands)
```typescript
let s = new Set();

function dfs(i: number, j: number, m: number, n: number, grid: string[][]): void {
  s.add(i * n &#43; j);
  if (i - 1 &gt;= 0 &amp;&amp; grid[i - 1][j] === &#34;1&#34; &amp;&amp; !s.has((i - 1) * n &#43; j)) dfs(i - 1, j, m, n, grid);
  if (i &#43; 1 &lt; m &amp;&amp; grid[i &#43; 1][j] === &#34;1&#34; &amp;&amp; !s.has((i &#43; 1) * n &#43; j)) dfs(i &#43; 1, j, m, n, grid);
  if (j - 1 &gt;= 0 &amp;&amp; grid[i][j - 1] === &#34;1&#34; &amp;&amp; !s.has(i * n &#43; (j - 1))) dfs(i, j - 1, m, n, grid);
  if (j &#43; 1 &lt; n &amp;&amp; grid[i][j &#43; 1] === &#34;1&#34; &amp;&amp; !s.has(i * n &#43; (j &#43; 1))) dfs(i, j &#43; 1, m, n, grid);
}

function numIslands(grid: string[][]): number {
  s = new Set();
  let res = 0;
  let m = grid.length, n = grid[0].length;

  for (let i = 0; i &lt; m; &#43;&#43;i) {
    for (let j = 0; j &lt; n; &#43;&#43;j) {
      if (grid[i][j] === &#34;1&#34; &amp;&amp; !s.has(i * n &#43; j)) {
        dfs(i, j, m, n, grid);
        &#43;&#43;res;
      }
    }
  }
  return res;
};

```

### [208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)
```typescript

interface trieNode {
  val: string;
  isEnd: boolean;
  sons: trieNode[];
};

class Trie {

  root: trieNode;

  constructor() {
    this.root = {
      val: &#34;&#34;,
      isEnd: false,
      sons: [],
    };
  }

  insert(word: string): void {
    let ptr = this.root;

    let len = word.length;
    for (let i = 0; i &lt; len; &#43;&#43;i) {

      let flag = false;

      let sons = ptr.sons;
      for (let son of sons) {
        if (son.val === word[i] &amp;&amp; (son.isEnd === false &amp;&amp; i &lt; len - 1 || son.isEnd === true &amp;&amp; i === len - 1)) {
          flag = true;
          ptr = son;
          break;
        }
      }
      if (!flag) {
        let newSon = {
          val: word[i],
          isEnd: i === len - 1 ? true : false,
          sons: [],
        };
        ptr.sons.push(newSon);
        ptr = newSon;
      }
    }
  }

  search(word: string): boolean {
    let res = true;

    let ptr = this.root;

    let len = word.length;
    for (let i = 0; i &lt; len; &#43;&#43;i) {

      let flag = false;

      let sons = ptr.sons;
      for (let son of sons) {
        if (son.val === word[i] &amp;&amp; (son.isEnd === false &amp;&amp; i &lt; len - 1 || son.isEnd === true &amp;&amp; i === len - 1)) {
          flag = true;
          ptr = son;
          break;
        }
      }
      if (!flag) {
        res = false;
        break;
      }
    }

    return res;
  }

  startsWith(prefix: string): boolean {
    let res = true;

    let ptr = this.root;

    let len = prefix.length;
    for (let i = 0; i &lt; len; &#43;&#43;i) {

      let flag = false;

      let sons = ptr.sons;
      for (let son of sons) {
        if (son.val === prefix[i] &amp;&amp; (son.isEnd === false &amp;&amp; i &lt; len - 1 || i === len - 1)) {
          flag = true;
          ptr = son;
          break;
        }
      }
      if (!flag) {
        res = false;
        break;
      }
    }

    return res;
  }
}
```

### [433. Minimum Genetic Mutation](https://leetcode.com/problems/minimum-genetic-mutation)
```typescript
let res = Infinity;

function diff(a: string, b: string): number {
  let res = 0;
  for (let i = 0; i &lt; 8; &#43;&#43;i) {
    if (a[i] !== b[i]) &#43;&#43;res;
  }
  return res;
}

function dfs(gene: string, endGene: string, bank: string[], depth: number, visited: Set&lt;string&gt;): void {
  if (gene === endGene) {
    if (depth &lt; res) res = depth;
    return;
  }
  for (let b of bank) {
    if (diff(gene, b) === 1 &amp;&amp; !visited.has(b)) {
      visited.add(b);
      dfs(b, endGene, bank, depth &#43; 1, visited);
      visited.delete(b);
    }
  }
}

function minMutation(startGene: string, endGene: string, bank: string[]): number {
  res = Infinity;
  dfs(startGene, endGene, bank, 0, new Set());
  if (res === Infinity) return -1;
  else return res;
};
```

### [77. Combinations](https://leetcode.com/problems/combinations)
```typescript
let res: number[][];

function dfs(n: number, k: number, nums: number[], left: number) {
  if (nums.length === k) {
    res.push(nums.slice());
    return;
  }

  for (let i = left; i &lt;= n; &#43;&#43;i) {
    nums.push(i);
    dfs(n, k, nums, i &#43; 1);
    nums.pop();
  }
}

function combine(n: number, k: number): number[][] {
  res = [];
  dfs(n, k, [], 1);
  return res;
};
```

### [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray)
```typescript
function maxSubArray(nums: number[]): number {
  let dp = [];
  let len = nums.length;
  let res = nums[0];
  dp[0] = nums[0];
  for (let i = 1; i &lt; len; &#43;&#43;i) {
    dp[i] = Math.max(nums[i], dp[i - 1] &#43; nums[i]);
    if (dp[i] &gt; res) res = dp[i];
  }
  return res;
};
```

### [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array)
```typescript
function findKthLargest(nums: number[], k: number): number {
  nums.sort((a, b) =&gt; b - a);
  return nums[k - 1];
};
```

### [267. Add Binary](https://leetcode.com/problems/add-binary)
```typescript
function addBinary(a: string, b: string): string {
  let x = BigInt(&#34;0b&#34; &#43; a);
  let y = BigInt(&#34;0b&#34; &#43; b);
  let z = x &#43; y;
  return z.toString(2);
};
```
### [50. Pow(x, n)](https://leetcode.com/problems/powx-n)
```typescript
function myPow(x: number, n: number): number {
  if (n &lt; 0) {
    x = 1 / x;
    n = -n;
  }

  let res = 1;
  while (n &gt; 0) {
    if (n % 2 === 1) res *= x;
    x *= x;
    n = Math.floor(n / 2);
  }

  return res;
};
```

### [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs)
```typescript
function climbStairs(n: number): number {
  let dp = [];
  dp[0] = 0;
  dp[1] = 1;
  dp[2] = 2;
  for (let i = 3; i &lt;= n; &#43;&#43;i) dp[i] = dp[i - 1] &#43; dp[i - 2];
  return dp[n];
};

```

### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)
```typescript
function maxProfit(prices: number[]): number {
  let p = [0];
  let len = prices.length;
  let max = 0;
  let sum = 0;
  let flag = false;
  for (let i = 1; i &lt; len; &#43;&#43;i) {
    p[i] = prices[i] - prices[i - 1];
    if (flag) {
      sum &#43;= p[i];
      if (sum &gt; max) max = sum;
      if (sum &lt;= 0) {
        sum = 0;
        flag = false;
      }
    } else {
      if (p[i] &gt; 0) {
        sum &#43;= p[i];
        if (sum &gt; max) max = sum;
        flag = true;
      }
    }
  }
  return max;
};
```

### [392. Is Subsequence](https://leetcode.com/problems/is-subsequence)
```typescript
function isSubsequence(s: string, t: string): boolean {
  let i = 0, j = 0;
  let l1 = s.length, l2 = t.length;
  while (i &lt; l1 &amp;&amp; j &lt; l2) {
    if (t[j] === s[i]) {
      &#43;&#43;i;
      &#43;&#43;j;
    } else &#43;&#43;j;
  }
  if (i &gt;= l1) return true;
  else return false;
};
```

### [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)
```typescript
function lengthOfLongestSubstring(s: string): number {
  let set = new Set();
  let res = 0, len = s.length, sum = 0;
  let t = &#34;&#34;;
  for (let i = 0; i &lt; len; &#43;&#43;i) {
    if (set.has(s[i])) {
      set.clear();
      let index = t.indexOf(s[i]);
      t = t.substring(index &#43; 1);
      for (let c of t) set.add(c);
      sum = t.length;
    }
    &#43;&#43;sum;
    t &#43;= s[i];
    set.add(s[i]);
    if (sum &gt; res) res = sum;
  }
  return res;
};
```

### [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix)
```typescript
function spiralOrder(matrix: number[][]): number[] {
  let sum = matrix.length * matrix[0].length;
  let cnt = 0;
  let i = 0, j = 0;
  let res = [];
  let right = true, down = false, left = false, up = false;
  while (true) {
    res.push(matrix[i][j]);
    &#43;&#43;cnt;
    matrix[i][j] = Infinity;
    if (cnt &gt;= sum) break;
    if (right) {
      if (j &#43; 1 &lt; matrix[0].length &amp;&amp; matrix[i][j &#43; 1] &lt;= 100) {
        j &#43;= 1;
        continue;
      } else {
        right = false;
        down = true;
      }
    }
    if (down) {
      if (i &#43; 1 &lt; matrix.length &amp;&amp; matrix[i &#43; 1][j] &lt;= 100) {
        i &#43;= 1;
        continue;
      } else {
        down = false;
        left = true;
      }
    }
    if (left) {
      if (j - 1 &gt;= 0 &amp;&amp; matrix[i][j - 1] &lt;= 100) {
        j -= 1;
        continue;
      } else {
        left = false;
        up = true;
      }
    }
    if (up) {
      if (i - 1 &gt;= 0 &amp;&amp; matrix[i - 1][j] &lt;= 100) {
        i -= 1;
        continue;
      } else {
        up = false;
        right = true;
      }
    }
    if (right) {
      if (j &#43; 1 &lt; matrix[0].length &amp;&amp; matrix[i][j &#43; 1] &lt;= 100) {
        j &#43;= 1;
        continue;
      } else {
        right = false;
        down = true;
      }
    }
  }
  return res;
};
```

### [290. Word Pattern](https://leetcode.com/problems/word-pattern)
```typescript
function wordPattern(pattern: string, s: string): boolean {
  let a = new Map(), b = new Map();
  let str = s.split(&#39; &#39;);
  if (pattern.length !== str.length) return false;
  let res = true;
  for (let i = 0; i &lt; pattern.length; &#43;&#43;i) {
    if (a.has(pattern[i])) {
      if (a.get(pattern[i]) !== str[i]) {
        res = false;
        break;
      }
    } else a.set(pattern[i], str[i]);
    if (b.has(str[i])) {
      if (b.get(str[i]) !== pattern[i]) {
        res = false;
        break;
      }
    } else b.set(str[i], pattern[i]);
  }
  return res;
};
```

### [56. Merge Intervals](https://leetcode.com/problems/merge-intervals)
```typescript
function merge(intervals: number[][]): number[][] {
  intervals.sort((a, b) =&gt; a[0] - b[0]);
  let res: number[][] = [];
  for (let i = 0; i &lt; intervals.length; &#43;&#43;i) {
    let len = res.length;
    if (len === 0 || res[len - 1][1] &lt; intervals[i][0]) res.push(intervals[i]);
    else res[len - 1][1] = Math.max(res[len - 1][1], intervals[i][1]);
  }
  return res;
};
```

### [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits)
```typescript
function hammingWeight(n: number): number {
  let s = n.toString(2);
  let res = 0;
  for (let c of s) {
    if (c === &#34;1&#34;) &#43;&#43;res;
  }
  return res;
};
```
### [202. Happy Number](https://leetcode.com/problems/happy-number)
```typescript
function isHappy(n: number): boolean {
  let num = n;
  let res = false;
  let rec: Set&lt;number&gt; = new Set();

  while (true) {
    if (num === 1) {
      res = true;
      break;
    }
    if (rec.has(num)) break;
    rec.add(num);
    let str = num.toString();
    num = 0;
    for (let c of str) num &#43;= Math.pow(&#43;c, 2);
  }

  return res;
};
```

### [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer)
```typescript
function romanToInt(s: string): number {
  let m: Map&lt;string, number&gt; = new Map();

  m.set(&#39;I&#39;, 1);
  m.set(&#39;V&#39;, 5);
  m.set(&#39;X&#39;, 10);
  m.set(&#39;L&#39;, 50);
  m.set(&#39;C&#39;, 100);
  m.set(&#39;D&#39;, 500);
  m.set(&#39;M&#39;, 1000);

  let res = 0;
  let ptr = 0;
  while (ptr &lt; s.length) {
    if (ptr === s.length - 1) {
      res &#43;= m.get(s[ptr])!;
      ptr &#43;= 1;
    } else {
      if (s[ptr] === &#39;I&#39;) {
        if (s[ptr &#43; 1] === &#39;V&#39;) {
          res &#43;= 4;
          ptr &#43;= 2;
        } else if (s[ptr &#43; 1] === &#39;X&#39;) {
          res &#43;= 9;
          ptr &#43;= 2;
        } else {
          res &#43;= 1;
          ptr &#43;= 1;
        }
      } else if (s[ptr] === &#39;X&#39;) {
        if (s[ptr &#43; 1] === &#39;L&#39;) {
          res &#43;= 40;
          ptr &#43;= 2;
        } else if (s[ptr &#43; 1] === &#39;C&#39;) {
          res &#43;= 90;
          ptr &#43;= 2;
        } else {
          res &#43;= 10;
          ptr &#43;= 1;
        }
      } else if (s[ptr] === &#39;C&#39;) {
        if (s[ptr &#43; 1] === &#39;D&#39;) {
          res &#43;= 400;
          ptr &#43;= 2;
        } else if (s[ptr &#43; 1] === &#39;M&#39;) {
          res &#43;= 900;
          ptr &#43;= 2;
        } else {
          res &#43;= 100;
          ptr &#43;= 1;
        }
      } else {
        res &#43;= m.get(s[ptr])!;
        ptr &#43;= 1;
      }
    }
  }
  return res;
};

```

### [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)
```typescript
function twoSum(numbers: number[], target: number): number[] {
  let left = 0, right = numbers.length - 1;
  while (left &lt; right) {
    let num = numbers[left] &#43; numbers[right]; 
    if (num === target) break;
    else if (num &lt; target) &#43;&#43;left;
    else --right;
  }
  return [left &#43; 1, right &#43; 1];
};
```

### [30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words)
```typescript
function findSubstring(s: string, words: string[]): number[] {
  let res: number[] = [];
  let wordLen = words[0].length;
  let len = wordLen * words.length;
  let left = 0;
  let end = s.length;
  let map: Map&lt;string, number&gt; = new Map();

  for (let word of words) {
    let cnt = map.get(word);
    if (!cnt) map.set(word, 1);
    else map.set(word, cnt &#43; 1);
  }

  while (left &lt; end) {
    if (left &#43; len &gt; end) break;
    let str = s.substring(left, left &#43; wordLen);
    if (map.has(str)) {

      let index = left &#43; wordLen;
      let m: Map&lt;string, number&gt; = new Map();
      m.set(str, 1);

      while (str.length &lt; len) {
        let newStr = s.substring(index, index &#43; wordLen);

        if (map.has(newStr) &amp;&amp; (!m.has(newStr) || m.get(newStr)! &lt; map.get(newStr)!)) {
          str &#43;= newStr;
          let cnt = m.get(newStr);
          if (!cnt) m.set(newStr, 1);
          else m.set(newStr, cnt &#43; 1);
          index &#43;= wordLen;
        }
        else break;
      }
      if (str.length === len) res.push(left);
    }
    &#43;&#43;left;
  }
  return res;
};
```

### [48. Rotate Image](https://leetcode.com/problems/rotate-image)
```typescript
function rotate(matrix: number[][]): void {
  let n = matrix.length;
  let m: number[][] = new Array(n).fill(undefined).map(
    () =&gt; new Array(n).fill(undefined)
  );
  for (let i = 0; i &lt; n; &#43;&#43;i) {
    for (let j = 0; j &lt; n; &#43;&#43;j) {
      m[i][j] = matrix[n - 1 - j][i];
    }
  }
  for (let i = 0; i &lt; n; &#43;&#43;i) {
    for (let j = 0; j &lt; n; &#43;&#43;j) {
      matrix[i][j] = m[i][j];
    }
  }
};
```

### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram)
```typescript
function isAnagram(s: string, t: string): boolean {
  if (s.length != t.length) return false;
  let res = true;
  let map: Map&lt;string, number&gt; = new Map();
  for (let char of s) {
    let cnt = map.get(char);
    if (!cnt) map.set(char, 1);
    else map.set(char, cnt &#43; 1);
  }
  for (let char of t) {
    if (!map.has(char) || map.get(char) === 0) {
      res = false;
      break;
    } else map.set(char, map.get(char)! - 1);
  }

  return res;
};
```


### [57. Insert Interval](https://leetcode.com/problems/insert-interval)
```typescript
function insert(intervals: number[][], newInterval: number[]): number[][] {
  if (intervals.length === 0) return [newInterval];
  let res: number[][] = [];
  let left = newInterval[0], right = newInterval[1];
  let flag = false;
  let inserted = false;
  for (let interval of intervals) {
    if (inserted) {
      res.push(interval);
      continue;
    }
    if (!flag) {
      if (interval[1] &lt; left) res.push(interval);
      else if (interval[0] &gt; right) {
        res.push(newInterval);
        res.push(interval);
        inserted = true;
      }
      else {
        left = Math.min(interval[0], left);
        right = Math.max(interval[1], right);
        flag = true;
      }
    } else {
      if (interval[0] &lt;= right) {
        right = Math.max(right, interval[1]);
      } else {
        res.push([left, right]);
        res.push(interval);
        flag = false;
        inserted = true;
      }
    }
  }
  if (!inserted) res.push([left, right]);

  return res;
};
```

### [155. Min Stack](https://leetcode.com/problems/min-stack)
```typescript
interface element {
  val: number;
  min: number;
}

class MinStack {

  min: number;
  len: number;
  stack: element[];

  constructor() {
    this.min = Infinity;
    this.stack = [];
    this.len = 0;
  }

  push(val: number): void {
    this.stack.push({ val: val, min: this.min });
    this.len &#43;= 1;
    if (val &lt; this.min) this.min = val;
  }

  pop(): void {
    this.min = this.stack[this.len - 1].min;
    this.stack.pop();
    this.len -= 1;
  }

  top(): number {
    return this.stack[this.len - 1].val;
  }

  getMin(): number {
    return this.min;
  }
}
```

### [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii)
```typescript
function deleteDuplicates(head: ListNode | null): ListNode | null {
  if (!head) return null;
  let res: ListNode | null = null;
  let map: Map&lt;number, number&gt; = new Map();
  let pos: ListNode | null = head, ptr: ListNode | null = null;

  while (pos) {
    let cnt = map.get(pos.val);
    if (!cnt) map.set(pos.val, 1);
    else map.set(pos.val, cnt &#43; 1);
    pos = pos.next;
  }

  pos = head;
  while (pos) {
    if (map.get(pos.val)! &gt; 1) pos = pos.next;
    else {
      if (!res) {
        res = pos;
        ptr = res;
      }
      else {
        ptr!.next = pos;
        ptr = ptr!.next;
      }
      pos = pos.next;
    }
  }
  if (ptr) ptr.next = null;

    return res;
};
```

### [100. Same Tree](https://leetcode.com/problems/same-tree)
```typescript
function dfs(i: TreeNode | null, j: TreeNode | null): boolean {
  if (!i &amp;&amp; !j) return true;
  else {
    if (i &amp;&amp; j &amp;&amp; i.val === j.val &amp;&amp; dfs(i.left, j.left) &amp;&amp; dfs(i.right, j.right)) return true;
    else return false;
  }
}

function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
  let i = p, j = q;
  return dfs(i, j);
};
```

### [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree)
```typescript
function dfs(node: TreeNode | null): void {
  if (!node) return;
  dfs(node.left);
  dfs(node.right);
  let tmp = node.left;
  node.left = node.right;
  node.right = tmp;
}

function invertTree(root: TreeNode | null): TreeNode | null {
  dfs(root);
  return root;
};
```

### [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree)
```typescript
interface node {
  val: number;
  isLeft: boolean;
}

let map: Map&lt;number, node&gt; = new Map();
let index = 0;

function dfs(n: TreeNode | null, isLeft: boolean): void {
  if (!n) return;
  &#43;&#43;index;
  map.set(index, { val: n.val, isLeft });

  dfs(n.left, true);
  dfs(n.right, false);
}

function dfs_1(n: TreeNode | null, isLeft: boolean): boolean {
  if (!n) return true;

  &#43;&#43;index;
  let s = map.get(index)!;

  return (s.val === n.val &amp;&amp; (index === 1 || s.isLeft != isLeft)) &amp;&amp; dfs_1(n.right, false) &amp;&amp; dfs_1(n.left, true);
}

function isSymmetric(root: TreeNode | null): boolean {
  if (!root) return true;
  map = new Map();
  index = 0;
  dfs(root, false);

  index = 0;
  return dfs_1(root, false);
};
```


### [112. Path Sum](https://leetcode.com/problems/path-sum)
```typescript
let flag = false;
let target = NaN;

function dfs(n: TreeNode | null, sum: number): void {
  if (flag || !n) return;

  sum &#43;= n.val;
  if (sum === target &amp;&amp; !n.left &amp;&amp; !n.right) {
    flag = true;
    return;
  }

  dfs(n.left, sum);
  dfs(n.right, sum);
}


function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
  flag = false;
  target = targetSum;
  dfs(root, 0);
  return flag;
};
```

### [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes)
```typescript
let res = 0;

function dfs(n: TreeNode | null): void {
  if (!n) return;
  &#43;&#43;res;
  dfs(n.left);
  dfs(n.right);
}

function countNodes(root: TreeNode | null): number {
  res = 0;
  dfs(root);
  return res;
};
```

### [222. Count Complete Tree Nodes](https://leetcode.com/problems/binary-tree-right-side-view)
```typescript
function rightSideView(root: TreeNode | null): number[] {
  let res = [];
  let q = [];

  if (root) {
    q.push(root);
    while (q.length &gt; 0) {
      res.push(q[q.length - 1].val);
      let len = q.length;
      while (len) {
        let n = q.shift();
        if (n!.left) q.push(n!.left);
        if (n!.right) q.push(n!.right);
        --len;
      }
    }
  }

  return res;
};
```

### [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree)
```typescript
let n: number[] = [];

function dfs(left: number, right: number): TreeNode | null {

  if (left === right) return null;

  let mid = Math.floor((left &#43; right) / 2);
  let e = new TreeNode(n[mid]);

  e.left = dfs(left, mid);
  e.right = dfs(mid &#43; 1, right);

  return e;
}

function sortedArrayToBST(nums: number[]): TreeNode | null {
  n = nums;
  return dfs(0, nums.length);
};
```

### [35. Search Insert Position](https://leetcode.com/problems/search-insert-position)
```typescript
function searchInsert(nums: number[], target: number): number {
  let res = 0;
  let left = 0, right = nums.length;

  while (left &lt; right) {
    let mid = Math.trunc((left &#43; right) / 2);
    if (nums[mid] &gt; target) right = mid;
    else if (nums[mid] &lt; target) left = mid &#43; 1;
    else {
      res = mid;
      break;
    }
    if (left === right) {
      res = left;
      break;
    }
  }

  return res;
};

```


### [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word)
```typescript
function lengthOfLastWord(s: string): number {
  let str = &#39;&#39;;
  let flag = false;
  for (let i = 0; i &lt; s.length; &#43;&#43;i) {
    if (!flag) {
      if (s[i] !== &#39; &#39;) {
        str = s[i];
        flag = true;
      }
    } else {
      if (s[i] === &#39; &#39;) flag = false;
      else str &#43;= s[i];
    }
  }
  return str.length;
};
```

### [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix)
```typescript
function longestCommonPrefix(strs: string[]): string {
  let str = strs[0];
  let len = str.length;
  let res = &#39;&#39;;

  for (let i = 0; i &lt;= len; &#43;&#43;i) {
    let sub = str.substring(0, i);

    let flag = true;
    for (let j = 0; j &lt; strs.length; &#43;&#43;j) {
      if (!strs[j].startsWith(sub)) {
        flag = false;
        break;
      }
    }
    if (flag) res = sub;
    else break;
  }
  return res;
};
```


### [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)
```typescript
function strStr(haystack: string, needle: string): number {
  return haystack.indexOf(needle);
};
```

### [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii)
```typescript
function containsNearbyDuplicate(nums: number[], k: number): boolean {
  let map: Map&lt;number, number[]&gt; = new Map();
  let res = false;

  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    let num = nums[i];

    if (map.has(num)) {
      let indexes = map.get(num)!;
      indexes!.push(i);
      map.set(num, indexes);
    } else {
      map.set(num, [i]);
    }
  }

  for (let p of map) {
    if (p[1].length &gt; 1) {
      let indexes = p[1];
      for (let i = 0; i &lt; nums.length - 1; &#43;&#43;i) {
        if (indexes[i &#43; 1] - indexes[i] &lt;= k) {
          res = true;
          break;
        }
      }
    }
    if (res === true) break;
  }

  return res;
};
```


### [190. Reverse Bits](https://leetcode.com/problems/reverse-bits)
```typescript
function reverseBits(n: number): number {
  let res = 0;
  for (let i = 0; i &lt; 32; &#43;&#43;i) {
    res = (res &lt;&lt; 1) | (n &amp; 1);
    n &gt;&gt;&gt;= 1;
  }
  return res &gt;&gt;&gt; 0;
};
```

### [136. Single Number](https://leetcode.com/problems/single-number)
```typescript
function singleNumber(nums: number[]): number {
  let res = 0;
  for (let num of nums) res ^= num;
  return res;
};
```

### [172. Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes)
```typescript
function trailingZeroes(n: number): number {
  let res = 0;
  while (n &gt; 0) {
    n = Math.trunc(n / 5);
    res &#43;= n;
  }
  return res;
};
```

### [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii)
```typescript
function removeDuplicates(nums: number[]): number {
  let cnt = 0;
  let n = 0;
  let index = 0;
  while (index &lt; nums.length) {
    let num = nums[index];
    if (n !== num) {
      n = num;
      cnt = 1
    } else &#43;&#43;cnt;
    if (cnt &gt;= 3) nums.splice(index, 1);
    else &#43;&#43;index;
  }
  return nums.length;
};

```

### [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water)
```typescript
function maxArea(height: number[]): number {
  let res = 0;
  let left = 0, right = height.length - 1;
  while (left &lt; right) {
    let area = (right - left) * Math.min(height[left], height[right]);
    if (area &gt; res) res = area;

    if (height[left] &lt;= height[right]) &#43;&#43;left;
    else --right;
  }

  return res;
};
```

### [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes)
```typescript
function setZeroes(matrix: number[][]): void {
  let rows = matrix.length, columns = matrix[0].length;
  let set: Set&lt;number&gt; = new Set();
  for (let i = 0; i &lt; rows; &#43;&#43;i) {
    for (let j = 0; j &lt; columns; &#43;&#43;j) {
      if (matrix[i][j] === 0 &amp;&amp; !set.has(i * columns &#43; j)) {
        for (let x = 0; x &lt; rows; &#43;&#43;x) {
          if (matrix[x][j] !== 0) {
            matrix[x][j] = 0;
            set.add(x * columns &#43; j);
          }
        }
        for (let y = 0; y &lt; columns; &#43;&#43;y) {
          if (matrix[i][y] !== 0) {
            matrix[i][y] = 0;
            set.add(i * columns &#43; y);
          }
        }
      }
    }
  }
};
```

### [49. Group Anagrams](https://leetcode.com/problems/group-anagrams)
```typescript
function groupAnagrams(strs: string[]): string[][] {
  let res: string[][] = [];
  let map: Map&lt;string, string[]&gt; = new Map();

  for (let i = 0; i &lt; strs.length; &#43;&#43;i) {
    let str = strs[i].split(&#39;&#39;);
    str.sort();
    let s = str.join(&#39;&#39;);
    if (map.has(s)) {
      let ss = map.get(s)!;
      ss.push(strs[i]);
      map.set(s, ss);
    } else map.set(s, [strs[i]]);
  }

  for (let p of map) res.push(p[1]);

  return res;
};
```

### [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons)
```typescript
function findMinArrowShots(points: number[][]): number {
  points.sort(
    (a, b): number =&gt; {
      return a[1] - b[1];
    }
  )
  let res = 1;
  let arrow = points[0][1];
  for (let i = 1; i &lt; points.length; &#43;&#43;i) {
    if (arrow &lt; points[i][0]) {
      &#43;&#43;res;
      arrow = points[i][1];
    }
  }
  return res;
};
```

### [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)
```typescript
function evalRPN(tokens: string[]): number {
  let s: number[] = [];
  for (let str of tokens) {
    let token = &#43;str;
    if (str !== &#39;&#43;&#39; &amp;&amp; str !== &#39;-&#39; &amp;&amp; str !== &#39;*&#39; &amp;&amp; str !== &#39;/&#39;) s.push(token);
    else {
      let b = s.pop()!;
      let a = s.pop()!;
      if (str === &#39;&#43;&#39;) s.push(a &#43; b);
      else if (str === &#39;-&#39;) s.push(a - b);
      else if (str === &#39;*&#39;) s.push(a * b);
      else s.push(Math.trunc(a / b));
    }
  }
  return s[0];
};
```

### [224. Basic Calculator](https://leetcode.com/problems/basic-calculator)
```typescript
function calculate(s: string): number {
  return eval(s);
};
```

### [86. Partition List](https://leetcode.com/problems/partition-list)
```typescript
function partition(head: ListNode | null, x: number): ListNode | null {
  if (!head) return null;

  let nodes: ListNode[] = [];
  let ptr: ListNode | null = head;
  while (ptr) {
    nodes.push(ptr);
    ptr = ptr.next;
  }
  nodes.sort((a, b) =&gt; {
    if (a.val &lt; x &amp;&amp; b.val &lt; x) return 0;
    else if (a.val &gt;= x &amp;&amp; b.val &gt;= x) return 0;
    else if (a.val &gt;= x &amp;&amp; b.val &lt; x) return 1;
    else return -1;
  });

  let res = nodes[0];
  ptr = res;
  
  for (let i = 1; i &lt; nodes.length; &#43;&#43;i) {
    ptr.next = nodes[i]!;
    ptr = ptr.next;
  }
  ptr.next = null;
  return res;
};
```

### [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)
```typescript
function buildTree(preorder: number[], inorder: number[]): TreeNode | null {

  if (preorder.length === 0) return null;

  let val = preorder[0];
  let root = new TreeNode(val);
  let mid = inorder.indexOf(val);

  root.left = buildTree(preorder.slice(1, mid &#43; 1), inorder.slice(0, mid));
  root.right = buildTree(preorder.slice(mid &#43; 1), inorder.slice(mid &#43; 1));

  return root;
};
```

### [106. Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal)
```typescript
function buildTree(inorder: number[], postorder: number[]): TreeNode | null {

  if (postorder.length === 0) return null;

  let val = postorder[postorder.length - 1];
  let root = new TreeNode(val);
  let mid = inorder.indexOf(val);

  root.left = buildTree(inorder.slice(0, mid), postorder.slice(0, mid));
  root.right = buildTree(inorder.slice(mid &#43; 1), postorder.slice(mid, -1));

  return root;
};
```

### [117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii)
```typescript
function connect(root: Node | null): Node | null {
  if (root === null) return root;

  let q: Node[] = [];

  q.push(root);

  while (q.length) {
    let len = q.length;
    for (let i = 0; i &lt; len - 1; &#43;&#43;i) q[i].next = q[i &#43; 1];
    for (let i = 0; i &lt; len; &#43;&#43;i) {
      let node = q.shift()!;
      if (node.left) q.push(node.left);
      if (node.right) q.push(node.right);
    }
  }

  return root;
};
```

### [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)
```typescript
let list: TreeNode[] = [];

function dfs(root: TreeNode): void {
  list.push(root);
  if (root.left) dfs(root.left);
  if (root.right) dfs(root.right);
}

function flatten(root: TreeNode | null): void {
  if (!root) return;

  list = [];
  dfs(root);

  let len = list.length - 1;
  for (let i = 0; i &lt; len; &#43;&#43;i) {
    list[i].right = list[i &#43; 1];
    list[i].left = null;
  }
  list[len].right = null;
  list[len].left = null;
};
```

### [129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers)
```typescript
let res: number = 0;

function dfs(root: TreeNode, num: string): void {
  num &#43;= root.val.toString();

  if (!root.left &amp;&amp; !root.right) {
    res &#43;= &#43;num;
    return;
  }

  if (root.left) dfs(root.left, num);
  if (root.right) dfs(root.right, num);
}

function sumNumbers(root: TreeNode | null): number {
  if (!root) return 0;

  res = 0;
  dfs(root, &#39;&#39;);

  return res;
};
```

### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)
```typescript
function levelOrder(root: TreeNode | null): number[][] {
  let res: number[][] = [];
  if (!root) return res;

  let q: TreeNode[] = [];
  q.push(root);

  while (q.length) {
    let list: number[] = [];
    let len = q.length;
    while (len) {
      let node = q.shift()!;
      list.push(node.val);
      if (node.left) q.push(node.left);
      if (node.right) q.push(node.right);
      --len;
    }
    res.push(list);
  }

  return res;
};
```

### [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst)
```typescript
let res: number = 0, target: number = 0, index: number = 0;

function dfs(root: TreeNode): void {
  if (root.left) dfs(root.left);

  &#43;&#43;index;
  if (index === target) {
    res = root.val;
    return;
  }

  if (root.right) dfs(root.right);
}

function kthSmallest(root: TreeNode | null, k: number): number {
  if (!root) return 0;

  res = 0;
  target = k;
  index = 0;

  dfs(root);

  return res;
};
```

### [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions)
```typescript
let set: Set&lt;string&gt; = new Set();

function dfs(x: number, y: number, m: number, n: number, board: string[][]): void {
  set.add(`${x},${y}`);
  if (x &#43; 1 &lt;= m - 1 &amp;&amp; board[x &#43; 1][y] === &#39;O&#39; &amp;&amp; !set.has(`${x &#43; 1},${y}`)) dfs(x &#43; 1, y, m, n, board);
  if (x - 1 &gt;= 0 &amp;&amp; board[x - 1][y] === &#39;O&#39; &amp;&amp; !set.has(`${x - 1},${y}`)) dfs(x - 1, y, m, n, board);
  if (y &#43; 1 &lt;= n - 1 &amp;&amp; board[x][y &#43; 1] === &#39;O&#39; &amp;&amp; !set.has(`${x},${y &#43; 1}`)) dfs(x, y &#43; 1, m, n, board);
  if (y - 1 &gt;= 0 &amp;&amp; board[x][y - 1] === &#39;O&#39; &amp;&amp; !set.has(`${x},${y - 1}`)) dfs(x, y - 1, m, n, board);
}


function solve(board: string[][]): void {
  set.clear();

  let m = board.length, n = board[0].length;

  for (let i = 0; i &lt; m; &#43;&#43;i) {
    if (board[i][0] === &#39;O&#39;) dfs(i, 0, m, n, board);
    if (board[i][n - 1] === &#39;O&#39;) dfs(i, n - 1, m, n, board);
  }
  for (let i = 0; i &lt; n; &#43;&#43;i) {
    if (board[0][i] === &#39;O&#39;) dfs(0, i, m, n, board);
    if (board[m - 1][i] === &#39;O&#39;) dfs(m - 1, i, m, n, board);
  }
  for (let i = 1; i &lt; m - 1; &#43;&#43;i) {
    for (let j = 1; j &lt; n - 1; &#43;&#43;j) {
      if (board[i][j] === &#39;O&#39; &amp;&amp; !set.has(`${i},${j}`)) board[i][j] = &#39;X&#39;;
    }
  }
};
```

### [909. Snakes and Ladders](https://leetcode.com/problems/snakes-and-ladders)
```typescript
function snakesAndLadders(board: number[][]): number {
  let n = board.length;

  let index = (x: number, y: number) =&gt; (n - 1 - x) * n &#43; ((n - 1 - x) % 2 === 1 ? n - y : y &#43; 1);
  let list: number[] = new Array(n * n &#43; 1).fill(-1);
  for (let i = 0; i &lt; n; &#43;&#43;i) {
    for (let j = 0; j &lt; n; &#43;&#43;j) {
      list[index(i, j)] = board[i][j];
    }
  }

  let map: Map&lt;number, number&gt; = new Map();
  let q: number[] = [];
  q.push(1);
  map.set(1, 0);

  while (q.length) {
    let node = q.shift()!;
    let end = Math.min(node &#43; 6, n * n);
    let step = map.get(node)!;
    for (let i = node &#43; 1; i &lt;= end; &#43;&#43;i) {
      if (list[i] === -1) {
        if (!map.has(i) || map.get(i)! &gt; step &#43; 1) {
          q.push(i);
          map.set(i, step &#43; 1);
        }
      } else {
        if (!map.has(list[i]) || map.get(list[i])! &gt; step &#43; 1) {
          q.push(list[i]);
          map.set(list[i], step &#43; 1);
        }
      }
    }
  }

  return map.get(n * n) || -1;
};
```

### [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure)
```typescript
class Char {
  char: string;
  next: Char[] | null;
  isEnd: boolean;
  constructor(char: string, isEnd: boolean) {
    this.char = char;
    this.next = null;
    this.isEnd = isEnd;
  }
}

class WordDictionary {

  root: Char;

  constructor() {
    this.root = new Char(&#39;&#39;, false);
  }

  dfs(node: Char, str: string): void {
    let char = str[0];
    let isEnd = str.length &gt; 1 ? false : true;

    let next: Char | null = null;
    if (!node.next) {
      node.next = [];
      next = new Char(char, isEnd);
      node.next.push(next);
    } else {
      for (let i = 0; i &lt; node.next.length; &#43;&#43;i) {
        if (node.next[i].char === char &amp;&amp; node.next[i].isEnd === isEnd) {
          next = node.next[i];
          break;
        }
      }
      if (!next) {
        next = new Char(char, isEnd);
        node.next.push(next);
      }
    }
    if (!isEnd) this.dfs(next, str.substring(1));
  }

  addWord(word: string): void {
    this.dfs(this.root, word);
  }

  search(word: string): boolean {
    let index = -1;
    let q: Char[] = [];
    q.push(this.root);

    while (q.length) {
      let char = word[index &#43; 1];
      let isEnd = index === word.length - 2 ? true : false;
      let len = q.length;
      let temp = index;
      for (let i = 0; i &lt; len; &#43;&#43;i) {
        let node = q.shift()!;
        if (char != &#39;.&#39;) {
          let flag = false;
          if (node.next) {
            for (let j = 0; j &lt; node.next.length; &#43;&#43;j) {
              if (node.next[j].char === char &amp;&amp; node.next[j].isEnd === isEnd) {
                flag = true;
                q.push(node.next[j]);
                break;
              }
            }
          }
          if (flag) index = temp &#43; 1;
        } else {
          if (node.next) {
            for (let j = 0; j &lt; node.next.length; &#43;&#43;j) {
              if (node.next[j].isEnd === isEnd) {
                q.push(node.next[j]);
                index = temp &#43; 1;
              }
            }
          }
        }
      }

    }
    return index === word.length - 1 ? true : false;
  }
}
```

### [46. Permutations](https://leetcode.com/problems/permutations)
```typescript
let res: number[][] = [];
let numbers: number[] = [];

function dfs(list: number[]): void {
  if (list.length === numbers.length) {
    res.push([...list]);
    return;
  }

  for (let i = 0; i &lt; numbers.length; &#43;&#43;i) {
    if (list.includes(numbers[i]) === false) {
      list.push(numbers[i]);
      dfs(list);
      list.pop();
    }
  }
}

function permute(nums: number[]): number[][] {
  res = [];
  numbers = nums;
  dfs([]);
  return res;
};
```

### [148. Sort List](https://leetcode.com/problems/sort-list)
```typescript
function sortList(head: ListNode | null): ListNode | null {
  if (!head) return null;
  let ptr: ListNode | null = head;
  let list: ListNode[] = [];

  while (ptr) {
    list.push(ptr);
    ptr = ptr.next;
  }

  list.sort((a, b) =&gt; a.val - b.val);

  ptr = list[0];
  for (let i = 0; i &lt; list.length - 1; &#43;&#43;i) list[i].next = list[i &#43; 1];
  list[list.length - 1].next = null;
  
  return ptr;
};
```

### [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix)
```typescript
function searchMatrix(matrix: number[][], target: number): boolean {
  let m = matrix.length, n = matrix[0].length;
  let up = 0, down = m, left = 0, right = n;
  let row = -1;

  while (up &lt; down) {
    let mid = Math.trunc((up &#43; down) / 2);
    if (matrix[mid][0] === target) return true;
    else if (matrix[mid][0] &lt; target) {
      if (mid &#43; 1 &gt;= m) {
        row = mid;
        break;
      }
      else if (matrix[mid &#43; 1][0] &gt;= target) {
        if (matrix[mid &#43; 1][0] === target) return true;
        row = mid;
        break;
      } else up = mid &#43; 1;
    } else {
      if (mid - 1 &lt; 0) return false;
      else if (matrix[mid - 1][0] &lt;= target) {
        if (matrix[mid - 1][0] === target) return true;
        row = mid - 1;
        break;
      } else down = mid;
    }
  }

  if (row === -1) return false;

  while (left &lt; right) {
    let mid = Math.trunc((left &#43; right) / 2);
    if (matrix[row][mid] === target) return true;
    else if (matrix[row][mid] &lt; target) left = mid &#43; 1;
    else right = mid;
  }


  return false;
};
```

### [137. Single Number II](https://leetcode.com/problems/single-number-ii)
```typescript
function singleNumber(nums: number[]): number {
  let once = 0, twice = 0;
  for (let i = 0; i &lt; nums.length; &#43;&#43;i) {
    once = ~twice &amp; (once ^ nums[i]);
    twice = ~once &amp; (twice ^ nums[i]);
  }
  return once;
};
```

### [201. Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range)
```typescript
function rangeBitwiseAnd(left: number, right: number): number {
  let res = left &amp; right;
  for (let i = left &#43; 1; i &lt; right; &#43;&#43;i) {
    res &amp;= i;
    if (res === 0) break;
  }
  return res;
};
```

### [149. Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line)
```typescript
function maxPoints(points: number[][]): number {
  if (points.length &lt; 3) return points.length;

  let res = 0;
  let x_1 = 0, y_1 = 0, x_2 = 0, y_2 = 0;
  let slope = 0, b = 0;

  for (let i = 0; i &lt; points.length; &#43;&#43;i) {
    for (let j = i &#43; 1; j &lt; points.length; &#43;&#43;j) {
      x_1 = points[i][0];
      y_1 = points[i][1];
      x_2 = points[j][0];
      y_2 = points[j][1];
      let cnt = 2;
      if (x_1 !== x_2) {
        slope = (y_1 - y_2) / (x_1 - x_2);
        b = y_1 - slope * x_1;
        for (let k = 0; k &lt; points.length; &#43;&#43;k) {
          if (k !== i &amp;&amp; k !== j) {
            if (Math.abs(points[k][0] * slope &#43; b - points[k][1]) &lt; 1e-9) &#43;&#43;cnt;
          }
        }
      } else {
        for (let k = 0; k &lt; points.length; &#43;&#43;k) {
          if (k !== i &amp;&amp; k !== j) {
            if (points[k][0] === x_1) &#43;&#43;cnt;
          }
        }
      }
      if (cnt &gt; res) res = cnt;
    }
  }
  return res;
};
```

### [198. House Robber](https://leetcode.com/problems/house-robber)
```typescript
function rob(nums: number[]): number {
  let dp: number[] = [];
  let len = nums.length;
  if (len === 1) return nums[0];

  dp[0] = nums[0];
  dp[1] = Math.max(dp[0], nums[1]);

  for (let i = 2; i &lt; len; &#43;&#43;i) {
    dp[i] = Math.max(dp[i - 1], dp[i - 2] &#43; nums[i]);
  }

  return dp[len - 1];
};
```

### [139. Word Break](https://leetcode.com/problems/house-robber)
```typescript
function wordBreak(s: string, wordDict: string[]): boolean {
  let set: Set&lt;string&gt; = new Set(wordDict);
  let len = s.length;
  let dp: boolean[] = new Array(len &#43; 1).fill(false);
  dp[0] = true;
  for (let i = 1; i &lt;= len; &#43;&#43;i) {
    for (let j = 0; j &lt; i; &#43;&#43;j) {
      if (dp[j]) {
        let word = s.substring(j, i);
        if (set.has(word)) dp[i] = true;
      }
    }
  }
  return dp[len];
};
```

### [189. Rotate Array](https://leetcode.com/problems/rotate-array)
```typescript
function rotate(nums: number[], k: number): void {
  let len = nums.length;
  k = k % len;
  for (let i = 0; i &lt; k; &#43;&#43;i) {
    let top = nums.pop()!;
    nums.splice(0, 0, top);
  }
};
```

### [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence)
```typescript
function longestConsecutive(nums: number[]): number {
  let set: Set&lt;number&gt; = new Set(nums);
  let res = 0;
  let cnt = 0;
  for (let num of nums) {
    if (!set.has(num - 1)) {
      cnt = 1;
      let i = num &#43; 1;
      while (set.has(i)) {
        &#43;&#43;cnt;
        &#43;&#43;i;
      }
      if (cnt &gt; res) res = cnt;
    }
  }
  return res;
};
```

### [15. 3Sum](https://leetcode.com/problems/3sum)
```typescript
function threeSum(nums: number[]): number[][] {
  let map: Map&lt;number, Set&lt;number&gt;&gt; = new Map();
  let res: number[][] = [];
  let s_1: Set&lt;string&gt; = new Set(), s_2: Set&lt;number&gt; = new Set();
  let len = nums.length;
  for (let i = 0; i &lt; len; &#43;&#43;i) {
    let set = map.get(nums[i]);
    if (set === undefined) {
      set = new Set();
      set.add(i);
      map.set(nums[i], set);
    }
    else set.add(i);
  }
  for (let i = 0; i &lt; len; &#43;&#43;i) {
    if (!s_2.has(nums[i])) {
      for (let j = i &#43; 1; j &lt; len; &#43;&#43;j) {
        let k = 0 - nums[i] - nums[j];
        let set = map.get(k);
        if (set !== undefined) {
          if (!(set.size === 0 || set.size === 1 &amp;&amp; (set.has(i) || set.has(j)) || set.size === 2 &amp;&amp; set.has(i) &amp;&amp; set.has(j))) {
            let indexes: number[] = [nums[i], nums[j], k];
            indexes.sort((a, b) =&gt; a - b);
            let str = indexes.toString();
            if (!s_1.has(str)) {
              s_1.add(str);
              res.push(indexes);
            }
          }
        }
      }
      s_2.add(nums[i]);
    }
  }
  return res;
};
```

### [236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree)
```typescript
let path_1: TreeNode[] = [], path_2: TreeNode[] = [];
let t_1 = 0, t_2 = 0;
let f_1 = false, f_2 = false;

function dfs(root: TreeNode) {
  if (f_1 &amp;&amp; f_2) return;
  if (!f_1) path_1.push(root);
  if (!f_2) path_2.push(root);

  if (root.val === t_1) f_1 = true;
  if (root.val === t_2) f_2 = true;

  if ((!f_1 || !f_2) &amp;&amp; root.left) dfs(root.left);
  if ((!f_1 || !f_2) &amp;&amp; root.right) dfs(root.right);

  if (!f_1) path_1.pop();
  if (!f_2) path_2.pop();
}

function lowestCommonAncestor(root: TreeNode | null, p: TreeNode | null, q: TreeNode | null): TreeNode | null {
  if (!root || !p || !q) return null;
  path_1 = [];
  path_2 = [];
  t_1 = p.val;
  t_2 = q.val;
  f_1 = false;
  f_2 = false;
  let res: TreeNode | null = root;
  let set: Set&lt;number&gt; = new Set();
  dfs(root);
  if (path_1.length &lt; path_2.length) {
    for (let t of path_2) set.add(t.val);
    for (let i = path_1.length - 1; i &gt;= 0; --i) {
      if (set.has(path_1[i].val)) {
        res = path_1[i];
        break;
      }
    }
  } else {
    for (let t of path_1) set.add(t.val);
    for (let i = path_2.length - 1; i &gt;= 0; --i) {
      if (set.has(path_2[i].val)) {
        res = path_2[i];
        break;
      }
    }
  }
  return res;
};
```

### [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)
```typescript
function maxProfit(prices: number[]): number {
  let result = 0;
  let sum = 0;
  for (let i = 1; i &lt; prices.length; &#43;&#43;i) {
    let p = prices[i] - prices[i - 1];
    if (p &gt; 0) sum &#43;= p;
    if (sum &gt; result) result = sum;
  }
  return result;
};
```

### [289. Game of Life](https://leetcode.com/problems/game-of-life)
```typescript
function gameOfLife(board: number[][]): void {
  let row = board.length, column = board[0].length;
  let newBoard: number[][] = new Array(row).fill(undefined).map(
    () =&gt; new Array(column).fill(undefined)
  );
  for (let i = 0; i &lt; row; &#43;&#43;i) {
    for (let j = 0; j &lt; column; &#43;&#43;j) {
      let n = 0;
      if (i - 1 &gt;= 0 &amp;&amp; board[i - 1][j] === 1) &#43;&#43;n;
      if (i &#43; 1 &lt; row &amp;&amp; board[i &#43; 1][j] === 1) &#43;&#43;n;
      if (j - 1 &gt;= 0 &amp;&amp; board[i][j - 1] === 1) &#43;&#43;n;
      if (j &#43; 1 &lt; column &amp;&amp; board[i][j &#43; 1] === 1) &#43;&#43;n;
      if (i - 1 &gt;= 0 &amp;&amp; j - 1 &gt;= 0 &amp;&amp; board[i - 1][j - 1] === 1) &#43;&#43;n;
      if (i - 1 &gt;= 0 &amp;&amp; j &#43; 1 &lt; column &amp;&amp; board[i - 1][j &#43; 1] === 1) &#43;&#43;n;
      if (i &#43; 1 &lt; row &amp;&amp; j - 1 &gt;= 0 &amp;&amp; board[i &#43; 1][j - 1] === 1) &#43;&#43;n;
      if (i &#43; 1 &lt; row &amp;&amp; j &#43; 1 &lt; column &amp;&amp; board[i &#43; 1][j &#43; 1] === 1) &#43;&#43;n;
      if (board[i][j] === 1) {
        if (n &lt; 2 || n &gt; 3) newBoard[i][j] = 0;
        else newBoard[i][j] = 1;
      } else {
        if (n === 3) newBoard[i][j] = 1;
        else newBoard[i][j] = 0;
      }
    }
  }
  for (let i = 0; i &lt; row; &#43;&#43;i) {
    for (let j = 0; j &lt; column; &#43;&#43;j) {
      board[i][j] = newBoard[i][j];
    }
  }
};
```

### [146. LRU Cache](https://leetcode.com/problems/lru-cache)
```typescript
interface LinkNode {
  prior: LinkNode | null;
  next: LinkNode | null;
  key: number;
};

class LRUCache {

  map: Map&lt;number, number&gt;;
  link: Map&lt;number, LinkNode&gt;;
  first: LinkNode | null;
  last: LinkNode | null;
  capacity: number;

  constructor(capacity: number) {
    this.map = new Map();
    this.link = new Map();
    this.first = null;
    this.last = null;
    this.capacity = capacity;
  }

  get(key: number): number {
    if (this.map.has(key)) {
      const value = this.map.get(key)!;
      let newFirst: LinkNode = this.link.get(key)!;
      if (this.first !== newFirst) {
        let priorOfNewFirst = newFirst.prior!;
        let nextOfNewFirst = newFirst.next;
        priorOfNewFirst.next = nextOfNewFirst;
        if (nextOfNewFirst) nextOfNewFirst.prior = priorOfNewFirst;
        if (this.last === newFirst) this.last = newFirst.prior;
        newFirst.prior = null;
        newFirst.next = this.first;
        this.first!.prior = newFirst;
        this.first = newFirst;
      }
      return value;
    } else return -1;
  }

  put(key: number, value: number): void {
    if (this.map.has(key)) {
      this.map.set(key, value);
      let newFirst: LinkNode = this.link.get(key)!;
      if (this.first !== newFirst) {
        let priorOfNewFirst = newFirst.prior!;
        let nextOfNewFirst = newFirst.next;
        priorOfNewFirst.next = nextOfNewFirst;
        if (nextOfNewFirst) nextOfNewFirst.prior = priorOfNewFirst;
        if (this.last === newFirst) this.last = newFirst.prior;
        newFirst.prior = null;
        newFirst.next = this.first;
        this.first!.prior = newFirst;
        this.first = newFirst;
      }
    } else {

      if (this.map.size &gt;= this.capacity) {
        let newRemoved = this.last!;
        this.last = newRemoved.prior;
        if (this.last) this.last.next = null;
        if (this.first === newRemoved) this.first = null;
        this.link.delete(newRemoved.key);
        this.map.delete(newRemoved.key);
      }

      this.map.set(key, value);
      let newFirst: LinkNode = { prior: null, next: this.first, key };
      if (this.first) this.first.prior = newFirst;
      this.first = newFirst;
      if (!this.last) this.last = newFirst;
      this.link.set(key, newFirst);
    }
  }
}
```

### [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseKGroup(head: ListNode | null, k: number): ListNode | null {
  if (!head || k === 1) return head;

  let list: ListNode[] = [];
  let ptr: ListNode | null = head;
  let result: ListNode | null = null;

  while (ptr) {
    list.push(ptr);
    ptr = ptr.next;
  }

  if (k &gt; list.length) return head;

  for (let i = k; i &lt;= list.length; i &#43;= k) {
    for (let j = i - 1; j &gt; i - k; --j) {
      list[j].next = list[j - 1];
    }
    if (i &#43; k &lt;= list.length) list[i - k].next = list[i &#43; k - 1];
    else if (i === list.length) list[i - k].next = null;
    else list[i - k].next = list[i];
  }

  result = list[k - 1];
  return result;
};
```

### [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseKGroup(head: ListNode | null, k: number): ListNode | null {
  if (!head || k === 1) return head;

  let ptr: ListNode | null = head;
  let result: ListNode | null = null;
  let len = 0;

  while (ptr) {
    len &#43;= 1;
    ptr = ptr.next;
  }

  if (k &gt; len) return head;

  let prior: ListNode | null = null;
  let tails: ListNode[] = [];
  ptr = head;
  let result: ListNode | null = null;

  for (let i = 0; i &lt; len; &#43;&#43;i) {
    if (i % k === 0) {
      if (len - i &gt;= k) tails.push(ptr);
      else {
        let tail = tails.shift();
        tail.next = ptr;
        break;
      }
    } else if ((i &#43; 1)% k === 0){
      if (tails.length === 0) result = ptr;
      else {
        let tail = tails.shift();
        tail.next = ptr;
      }
      ptr.next = prior;
    } else ptr.next = prior;

    prior = ptr;
  }

  if (tails.length) {
    let tail = tails.shift();
    tail.next = null;
  }

  return result;
};
```

### [322. Coin Change](https://leetcode.com/problems/coin-change)
```javascript
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
function coinChange(coins, amount) {
  let dp = Array(amount &#43; 1).fill(Infinity);
  dp[0] = 0;

  for (let i = 1; i &lt; dp.length; &#43;&#43;i) {
    for (let j = 0; j &lt; coins.length; &#43;&#43;j) {
      if (i - coins[j] &gt;= 0) dp[i] = Math.min(dp[i], dp[i - coins[j]] &#43; 1);
    }
  }

  return dp[amount] === Infinity ? -1 : dp[amount];
};
```

### [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence)
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function (nums) {
  if (nums.length === 1) return 1;

  let dp = Array(nums.length).fill(1);

  dp[dp.length - 1] = 1;

  let res = 0;

  for (let i = dp.length - 2; i &gt;= 0; --i) {
    let max = 0;
    for (let j = i &#43; 1; j &lt; dp.length; &#43;&#43;j) {
      if (nums[j] &gt; nums[i]) {
        if (dp[j] &#43; 1 &gt; max) max = dp[j] &#43; 1;
      }
    }
    dp[i] = Math.max(max, dp[i]);

    res = Math.max(res, dp[i]);
  }

  return res;
};
```

### [120. Triangle](https://leetcode.com/problems/longest-increasing-subsequence)
```javascript
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function (triangle) {
  let dp = [];
  for (let i = 0; i &lt; triangle.length; &#43;&#43;i) {
    dp.push(Array(triangle[i].length).fill(Infinity));
  }

  dp[0][0] = triangle[0][0];

  for (let i = 1; i &lt; triangle.length; &#43;&#43;i) {
    for (let j = 0; j &lt; triangle[i].length; &#43;&#43;j) {
      if (j === triangle[i].length - 1) dp[i][j] = dp[i - 1][j - 1] &#43; triangle[i][j];
      else if (j === 0) dp[i][j] = dp[i - 1][j] &#43; triangle[i][j];
      else dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j]) &#43; triangle[i][j];
    }
  }

  let res = Infinity;
  for (let i = 0; i &lt; dp[dp.length - 1].length; &#43;&#43;i) {
    res = Math.min(res, dp[dp.length - 1][i]);
  }
  return res;
};
```


---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/recent-leetcode-top-interview-150-problem-solving-record/  

