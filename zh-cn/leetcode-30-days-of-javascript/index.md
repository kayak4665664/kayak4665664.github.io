# LeetCode: 30 Days of JavaScript


{{&lt; link href=&#34;https://leetcode.com/studyplan/30-days-of-javascript/&#34; content=&#34;30 Days of JavaScript&#34; title=&#34;30 Days of JavaScript&#34; card=true &gt;}}

&lt;!--more--&gt;

## [2667. Create Hello World Function](https://leetcode.com/problems/create-hello-world-function)
```javascript
/**
 * @return {Function}
 */
var createHelloWorld = function() {
    
    return function(...args) {
        return &#34;Hello World&#34;;
    }
};

/**
 * const f = createHelloWorld();
 * f(); // &#34;Hello World&#34;
 */
```

## [2623. Memoize](https://leetcode.com/problems/memoize)
```javascript
/**
 * @param {Function} fn
 * @return {Function}
 */
function memoize(fn) {

  const memory = new Map();

  return function (...args) {
    let key = fn.name;
    for (let arg of args) key &#43;= &#39;.&#39; &#43; arg;

    if (memory.has(key)) return memory.get(key);
    else {
      const value = fn(...args);
      memory.set(key, value);
      return value;
    }
  }
}


/** 
* let callCount = 0;
* const memoizedFn = memoize(function (a, b) {
*	 callCount &#43;= 1;
*   return a &#43; b;
* })
* memoizedFn(2, 3) // 5
* memoizedFn(2, 3) // 5
* console.log(callCount) // 1 
*/
```

## [2637. Promise Time Limit](https://leetcode.com/problems/promise-time-limit)
```javascript
/**
 * @param {Function} fn
 * @param {number} t
 * @return {Function}
 */
var timeLimit = function (fn, t) {

  return async function (...args) {

    const timeoutPromise = new Promise((_, reject) =&gt; {
      setTimeout(() =&gt; {
        reject(&#34;Time Limit Exceeded&#34;);
      }, t);
    });

    return Promise.race([fn(...args), timeoutPromise]);
  }
};

/**
* const limited = timeLimit((t) =&gt; new Promise(res =&gt; setTimeout(res, t)), 100);
* limited(150).catch(console.log) // &#34;Time Limit Exceeded&#34; at t=100ms
*/
```

## [2703. Return Length of Arguments Passed](https://leetcode.com/problems/return-length-of-arguments-passed)
```javascript
/**
 * @param {...(null|boolean|number|string|Array|Object)} args
 * @return {number}
 */
var argumentsLength = function (...args) {
  return args.length;
};

/**
 * argumentsLength(1, 2, 3); // 3
 */
```

## [2629. Function Composition](https://leetcode.com/problems/return-length-of-arguments-passed)
```javascript
/**
 * @param {Function[]} functions
 * @return {Function}
 */
var compose = function (functions) {

  return function (x) {
    if (functions.length === 0) return x;
    else {
      let res = functions[functions.length - 1](x);
      for (let i = functions.length - 2; i &gt;= 0; --i) res = functions[i](res);
      return res;
    }
  }
};

/**
* const fn = compose([x =&gt; x &#43; 1, x =&gt; 2 * x])
* fn(4) // 9
*/
```

## [2622. Cache With Time Limit](https://leetcode.com/problems/cache-with-time-limit)
```javascript
var TimeLimitedCache = function () {
  this.cache = new Map();
  this.timer = new Map();
};

/** 
 * @param {number} key
 * @param {number} value
 * @param {number} duration time until expiration in ms
 * @return {boolean} if un-expired key already existed
 */
TimeLimitedCache.prototype.set = function (key, value, duration) {
  const keyExists = this.cache.has(key);

  if (keyExists) {
    clearTimeout(this.timer.get(key));
  }

  this.cache.set(key, value);

  const timer = setTimeout(() =&gt; {
    this.cache.delete(key);
    this.timer.delete(key);
  }, duration);

  this.timer.set(key, timer);

  return keyExists;
};

/** 
 * @param {number} key
 * @return {number} value associated with key
 */
TimeLimitedCache.prototype.get = function (key) {
  if (this.cache.has(key)) {
    return this.cache.get(key);
  } else {
    return -1;
  }
};

/** 
 * @return {number} count of non-expired keys
 */
TimeLimitedCache.prototype.count = function () {
  return this.cache.size;
};

/**
 * const timeLimitedCache = new TimeLimitedCache()
 * timeLimitedCache.set(1, 42, 1000); // false
 * timeLimitedCache.get(1) // 42
 * timeLimitedCache.count() // 1
 */

```

## [2627. Debounce](https://leetcode.com/problems/debounce)
```javascript
/**
 * @param {Function} fn
 * @param {number} t milliseconds
 * @return {Function}
 */
var debounce = function (fn, t) {

  let timer = null;

  return function (...args) {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() =&gt; {
      fn(...args);
    }, t);
  }
};

/**
* const log = debounce(console.log, 100);
* log(&#39;Hello&#39;); // cancelled
* log(&#39;Hello&#39;); // cancelled
* log(&#39;Hello&#39;); // Logged at t=100ms
*/
```

## [2721. Execute Asynchronous Functions in Parallel](https://leetcode.com/problems/execute-asynchronous-functions-in-parallel)
```javascript
/**
 * @param {Array&lt;Function&gt;} functions
 * @return {Promise&lt;any&gt;}
 */
var promiseAll = function (functions) {
  return new Promise((resolve, reject) =&gt; {
    const results = [];
    let cnt = 0;

    functions.forEach((func, index) =&gt; {
      func().then((res) =&gt; {
        results[index] = res;
        &#43;&#43;cnt;

        if (cnt === functions.length) resolve(results);

      }).catch((err) =&gt; {
        reject(err);
      })
    })
  })
};

/**
 * const promise = promiseAll([() =&gt; new Promise(res =&gt; res(42))])
 * promise.then(console.log); // [42]
 */
```

## [2723. Add Two Promises](https://leetcode.com/problems/add-two-promises)
```javascript
/**
 * @param {Promise} promise1
 * @param {Promise} promise2
 * @return {Promise}
 */
var addTwoPromises = async function (promise1, promise2) {
  const a = await promise1;
  const b = await promise2;
  return a &#43; b;
};

/**
 * addTwoPromises(Promise.resolve(2), Promise.resolve(2))
 *   .then(console.log); // 4
 */
```

## [2621. Sleep](https://leetcode.com/problems/sleep)
```javascript
/**
 * @param {number} millis
 * @return {Promise}
 */
async function sleep(millis) {
  return new Promise((resolve, reject) =&gt; {
    setTimeout(() =&gt; { resolve(0) }, millis);
  });
}

/** 
 * let t = Date.now()
 * sleep(100).then(() =&gt; console.log(Date.now() - t)) // 100
 */
```

## [2715. Timeout Cancellation](https://leetcode.com/problems/timeout-cancellation)
```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function (fn, args, t) {
  const flag = true;

  setTimeout(() =&gt; {
    if (flag) fn(...args);
  }, t);

  return function () {
    flag = false;
  }
};

/**
 *  const result = [];
 *
 *  const fn = (x) =&gt; x * 5;
 *  const args = [2], t = 20, cancelTimeMs = 50;
 *
 *  const start = performance.now();
 *
 *  const log = (...argsArr) =&gt; {
 *      const diff = Math.floor(performance.now() - start);
 *      result.push({&#34;time&#34;: diff, &#34;returned&#34;: fn(...argsArr)});
 *  }
 *       
 *  const cancel = cancellable(log, args, t);
 *
 *  const maxT = Math.max(t, cancelTimeMs);
 *           
 *  setTimeout(cancel, cancelTimeMs);
 *
 *  setTimeout(() =&gt; {
 *      console.log(result); // [{&#34;time&#34;:20,&#34;returned&#34;:10}]
 *  }, maxT &#43; 15)
 */
```

## [2725. Interval Cancellation](https://leetcode.com/problems/interval-cancellation)
```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function (fn, args, t) {
  fn(...args);

  const timer = setInterval(() =&gt; {
    fn(...args);
  }, t);

  return function () {
    clearInterval(timer);
  }
};

/**
 *  const result = [];
 *
 *  const fn = (x) =&gt; x * 2;
 *  const args = [4], t = 35, cancelTimeMs = 190;
 *
 *  const start = performance.now();
 *
 *  const log = (...argsArr) =&gt; {
 *      const diff = Math.floor(performance.now() - start);
 *      result.push({&#34;time&#34;: diff, &#34;returned&#34;: fn(...argsArr)});
 *  }
 *       
 *  const cancel = cancellable(log, args, t);
 *
 *  setTimeout(cancel, cancelTimeMs);
 *   
 *  setTimeout(() =&gt; {
 *      console.log(result); // [
 *                           //     {&#34;time&#34;:0,&#34;returned&#34;:8},
 *                           //     {&#34;time&#34;:35,&#34;returned&#34;:8},
 *                           //     {&#34;time&#34;:70,&#34;returned&#34;:8},
 *                           //     {&#34;time&#34;:105,&#34;returned&#34;:8},
 *                           //     {&#34;time&#34;:140,&#34;returned&#34;:8},
 *                           //     {&#34;time&#34;:175,&#34;returned&#34;:8}
 *                           // ]
 *  }, cancelTimeMs &#43; t &#43; 15)    
 */
```

## [2631. Group By](https://leetcode.com/problems/group-by)
```javascript
/**
 * @param {Function} fn
 * @return {Object}
 */
Array.prototype.groupBy = function (fn) {
  const res = {};

  for (let i = 0; i &lt; this.length; &#43;&#43;i) {
    const key = fn(this[i]);
    if (res[key]) res[key].push(this[i]);
    else res[key] = [this[i]];
  }

  return res;
};

/**
 * [1,2,3].groupBy(String) // {&#34;1&#34;:[1],&#34;2&#34;:[2],&#34;3&#34;:[3]}
 */
```

## [2625. Flatten Deeply Nested Array](https://leetcode.com/problems/flatten-deeply-nested-array)
```javascript
/**
 * @param {Array} arr
 * @param {number} depth
 * @return {Array}
 */
// var flat = function (arr, n) {

//   if (n === 0) return arr;

//   return arr.reduce((res, item) =&gt; {
//     if (Array.isArray(item)) return res.concat(flat(item, n - 1));
//     else return res.concat(item);
//   }, []);
// };

var flat = function (arr, n) {
  if (n === 0) return arr;

  const res = [];
  const stack = arr.map(a =&gt; [a, n]);

  while (stack.length) {
    const [cur, depth] = stack.pop();

    if (Array.isArray(cur) &amp;&amp; depth &gt; 0) {
      stack.push(...cur.map(c =&gt; [c, depth - 1]));
    } else {
      res.push(cur);
    }
  }

  return res.reverse();
};

```

## [2705. Compact Object](https://leetcode.com/problems/compact-object)
```javascript
/**
 * @param {Object|Array} obj
 * @return {Object|Array}
 */
var compactObject = function (obj) {
  if (Array.isArray(obj)) {
    let i = 0;
    while (i &lt; obj.length) {
      if (Array.isArray(obj[i]) || obj[i] instanceof Object) {
        obj[i] = compactObject(obj[i]);
      }
      if (Boolean(obj[i]) === false) obj.splice(i, 1);
      else &#43;&#43;i;
    }
    return obj;
  } else {
    let keys = Object.keys(obj);
    for (let key of keys) {
      let value = obj[key];
      if (Array.isArray(value) || value instanceof Object) {
        value = compactObject(value);
      }
      if (Boolean(value) === false) delete obj[key];
    }
    return obj;
  }
};
```

## [2694. Event Emitter](https://leetcode.com/problems/event-emitter)
```javascript
class EventEmitter {

  constructor() {
    this.event = new Map();
  }

  /**
   * @param {string} eventName
   * @param {Function} callback
   * @return {Object}
   */
  subscribe(eventName, callback) {

    let callbacks = undefined;

    if (this.event.has(eventName)) {
      callbacks = this.event.get(eventName);
    } else {
      callbacks = [];
    }

    callbacks.push(callback);
    this.event.set(eventName, callbacks);

    const index = callbacks.length - 1;

    return {
      unsubscribe: () =&gt; {
        if (this.event.has(eventName)) {
          const callbacks = this.event.get(eventName);
          callbacks[index] = null;
          this.event.set(eventName, callbacks);
        }
      }
    };
  }

  /**
   * @param {string} eventName
   * @param {Array} args
   * @return {Array}
   */
  emit(eventName, args = []) {
    if (this.event.has(eventName)) {
      const results = [];

      const callbacks = this.event.get(eventName);

      for (let callback of callbacks) {
        if (callback !== null) {
          const res = callback(...args);
          results.push(res);
        }
      }

      return results;
    } else return [];
  }
}

/**
* const emitter = new EventEmitter();
*
* // Subscribe to the onClick event with onClickCallback
* function onClickCallback() { return 99 }
* const sub = emitter.subscribe(&#39;onClick&#39;, onClickCallback);
*
* emitter.emit(&#39;onClick&#39;); // [99]
* sub.unsubscribe(); // undefined
* emitter.emit(&#39;onClick&#39;); // []
*/
```

## [2722. Join Two Arrays by ID](https://leetcode.com/problems/join-two-arrays-by-id)
```javascript
/**
 * @param {Array} arr1
 * @param {Array} arr2
 * @return {Array}
 */
var join = function (arr1, arr2) {

  const res = [];
  const map = new Map();

  for (let obj of arr1) map.set(obj.id, { ...obj });

  for (let obj of arr2) {
    const id = obj.id;

    if (map.has(id)) {
      const o = map.get(id);
      for (let key in obj) o[key] = obj[key];
    } else map.set(id, { ...obj });
  }

  for (let value of map.values()) res.push(value);

  res.sort((a, b) =&gt; a.id - b.id);

  return res;
};
```

## [2695. Array Wrapper](https://leetcode.com/problems/array-wrapper)
```javascript
/**
 * @param {number[]} nums
 * @return {void}
 */
var ArrayWrapper = function (nums) {
  this.nums = [...nums]
};

/**
 * @return {number}
 */
ArrayWrapper.prototype.valueOf = function () {
  if (this.nums.length === 0) return 0;

  return this.nums.reduce((sum, num) =&gt; {
    return sum &#43; num
  }, 0);
}

/**
 * @return {string}
 */
ArrayWrapper.prototype.toString = function () {
  let str = &#39;[&#39;;

  for (const num of this.nums) {
    if (str !== &#39;[&#39;) str &#43;= &#39;,&#39;;
    str &#43;= num;
  }
  
  return str &#43; &#39;]&#39;;
}

/**
 * const obj1 = new ArrayWrapper([1,2]);
 * const obj2 = new ArrayWrapper([3,4]);
 * obj1 &#43; obj2; // 10
 * String(obj1); // &#34;[1,2]&#34;
 * String(obj2); // &#34;[3,4]&#34;
 */
```

## [2726. Calculator with Method Chaining](https://leetcode.com/problems/calculator-with-method-chaining)
```javascript
class Calculator {

  /** 
   * @param {number} value
   */
  constructor(value) {
    this.value = value;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  add(value) {
    this.value &#43;= value;
    return this;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  subtract(value) {
    this.value -= value;
    return this;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  multiply(value) {
    this.value *= value;
    return this;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  divide(value) {
    if (value === 0) throw new Error(&#34;Division by zero is not allowed&#34;);

    this.value /= value;
    return this;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  power(value) {
    this.value = Math.pow(this.value, value);
    return this;
  }

  /** 
   * @return {number}
   */
  getResult() {
    return this.value;
  }
}
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/leetcode-30-days-of-javascript/  

