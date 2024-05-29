# Stacks and Queues

## Easy Problem

## 1. 496. Next Greater Element I

### Solution 1

### Time O(M * N) and Space Complexity O(M)
```
*var nextGreaterElement = function (nums1, nums2) {
    let ans = [];

    for (let i = 0; i < nums1.length; i++) {
        let isFound = false;
        let num = nums1[i];
        let index = nums2.indexOf(num);
        for (let j = index; j < nums2.length; j++) {
            if (nums2[j] > num) {
                ans.push(nums2[j]);
                isFound = true;
                break;
            }
        }

        if (!isFound) ans.push(-1);
    }
    return ans;
};
```

### Solution 2

### Time O(M + N) and Space Complexity O(M)

```
var nextGreaterElement = function (nums1, nums2) {
    let ans = [];
    let stack = [];
    let map = new Map();

    nums2.forEach((num) => {
        while (stack.length > 0 && stack[stack.length - 1] < num) {
            map.set(stack.pop(), num);
        }
        stack.push(num);
    });

    return nums1.map((n) => map.get(n) ?? -1);
}   
```

***

## 2. 1021. Remove Outermost Parentheses
### Time  O(N) and Space Complexity O(N)

```
/**
 * @param {string} s
 * @return {string}
 */
var removeOuterParentheses = function (s) {
    let stack = [];
    let length = stack.length;
    const objList = {
        '(': ')',
    }

    for (let char of s) {
        if (char in objList) {
            if (length) {
                stack.push(char)
            }
            length += 1;
        } else {
            length -= 1
            if (length) {
                stack.push(char)
            }
        }
    }
    return stack.join("");
};
```

***

## 3. 1047. Remove All Adjacent Duplicates In String
[https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/description/](url)
### Time  O(N) and Space Complexity O(N)

```
/**
 * @param {string} s
 * @return {string}
 */
var removeDuplicates = function (s) {
    let stack = [];
    for(let char of s){
        if(stack[stack.length - 1] == char) {
            stack.pop();
        } else {
            stack.push(char);
        }
    }
   

    return stack.join("");
};
```

***

## 4. 933. Number of Recent Calls
[https://leetcode.com/problems/number-of-recent-calls/description/](url)
### Time  O(N) and Space Complexity O(N)

```

var RecentCounter = function() {
    this.timestamps = [];
};

/** 
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function(t) {
    this.timestamps.push(t);
    while(this.timestamps[0] < t- 3000){
            this.timestamps.shift() // remove the timestamps which is less than the requested one.
    }

    return this.timestamps.length;
    
};

/** 
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```

***

## 5. [https://practice.geeksforgeeks.org/problems/reverse-first-k-elements-of-queue/1/](url)

## 6. [https://practice.geeksforgeeks.org/problems/delete-middle-element-of-a-stack/1/](url)

## 7. [https://practice.geeksforgeeks.org/problems/inorder-traversal-iterative/1/](url)

## 8. [https://practice.geeksforgeeks.org/problems/preorder-traversal-iterative/1/](url)

## 9. 733. Flood Fill
[https://leetcode.com/problems/flood-fill/description/](url)
### ### Time  O(N) and Space Complexity O(N)

```
/**
 * @param {number[][]} image
 * @param {number} sr
 * @param {number} sc
 * @param {number} color
 * @return {number[][]}
 */
const floodFill = (image, sr, sc, newColor, firstColor = image[sr][sc]) => {
    // handle if the coordinate is out of bounds
    if (sr < 0 || sc < 0 || sr >= image.length || sc >= image[sr].length || image[sr][sc] !== firstColor || image[sr][sc] === newColor)   {
        return image; // return image as-is
    }
    
    image[sr][sc] = newColor;
    
    floodFill(image, sr + 1, sc, newColor, firstColor);
    floodFill(image, sr - 1, sc, newColor, firstColor);
    floodFill(image, sr, sc + 1, newColor, firstColor);
    floodFill(image, sr, sc - 1, newColor, firstColor);
    
	// return modified image
    return image;
};
```

***

## 10. 232. Implement Queue using Stacks
[https://leetcode.com/problems/implement-queue-using-stacks/description/](url)

### Solution 1
### Time Except Pop() others are O(1) and Space Complexity O(N)

```

var MyQueue = function() {
    this.queue = [];
};

/** 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function(x) {
    this.queue.push(x);
};

/**
 * @return {number}
 */
MyQueue.prototype.pop = function() {
    return this.queue.shift();
};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function() {
    return this.queue[0];
};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function() {
    return this.queue.length == 0;
};

/** 
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```

### Solution 2
### Time O(1) and Space Complexity O(N)

```

var MyQueue = function() {
    this.s1 = [], this.s2 = [];
};

/** 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function(x) {
    while(this.s1.length){
        this.s2.push(this.s1.pop()); //reverse push the elements
    }

    this.s1.push(x); // push the primary stack;

    while(this.s2.length){
        this.s1.push(this.s2.pop()); // push back the elements reverse order.
    }
};

/**
 * @return {number}
 */
MyQueue.prototype.pop = function() {
    return this.s1.pop();
};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function() {
    return this.s1[this.s1.length - 1];
};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function() {
    return this.s1.length == 0;
};

/** 
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```

***



## Medium Problems

## 1. 155. Min Stack

### Solution 1
### Time Everything is O(1) except getMin and Space Complexity O(N)

```
var MinStack = function() {
    this.stack = [];
};

/** 
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function(val) {
    this.stack.push(val);
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    this.stack.pop();
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    return this.stack[this.stack.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
    return Math.min(...this.stack);
};

/** 
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```

### Solution 2
### Time Everything is O(1) and Space Complexity O(N)

```
var MinStack = function() {
  this.stack = [];
};

MinStack.prototype.push = function(val) {
  if (this.stack.length === 0) {
    this.stack.push({ val: val, min: val });
  } else {
    var min = Math.min(this.stack[this.stack.length - 1].min, val);
    this.stack.push({ val: val, min: min });
  }
};

MinStack.prototype.pop = function() {
  if (this.stack.length > 0) {
    this.stack.pop();
  }
};

MinStack.prototype.top = function() {
  if (this.stack.length > 0) {
    return this.stack[this.stack.length - 1].val;
  }
  return null;
};

MinStack.prototype.getMin = function() {
  if (this.stack.length > 0) {
    return this.stack[this.stack.length - 1].min;
  }
  return null;
};

```

***

## 2. 1381. Design a Stack With Increment Operation

### Solution 1
###  Time complexity:
### Pop O(1)
### Push O(1)
### Increment O(n) n = value of k or stack.length which is minimum
### Space complexity: O(n)

```
/**
 * @param {number} maxSize
 */
var CustomStack = function(maxSize) {
    this.stack = [];
    this.maxSize = maxSize;
};

/** 
 * @param {number} x
 * @return {void}
 */
CustomStack.prototype.push = function(x) {
    if(this.stack.length < this.maxSize) this.stack.push(x);
};

/**
 * @return {number}
 */
CustomStack.prototype.pop = function() {
    return (this.stack.length == 0) ? -1 : this.stack.pop();
};

/** 
 * @param {number} k 
 * @param {number} val
 * @return {void}
 */
CustomStack.prototype.increment = function(k, val) {
    let length = (k < this.stack.length) ? k : this.stack.length;

    if(length == 0) return;

    for(let i = 0; i < length; i++){
        this.stack[i] += val;
    }
};

/** 
 * Your CustomStack object will be instantiated and called as such:
 * var obj = new CustomStack(maxSize)
 * obj.push(x)
 * var param_2 = obj.pop()
 * obj.increment(k,val)
 */
```

***

## 3. 921. Minimum Add to Make Parentheses Valid

### Solution 1

### Time Everything is O(N) and Space Complexity O(N)


```
/**
 * @param {string} s
 * @return {number}
 */
var minAddToMakeValid = function(s) {
    if(s == "") return 0;

    let stack = [];

    for(let i = 0; i < s.length; i++){
        if(s[i] == ")" && stack[stack.length - 1] == "(") {
            stack.pop();
        } else {
            stack.push(s[i]);
        }
    }

    return stack.length;
};
```

### Solution 2

### Time Everything is O(N) and Space Complexity O(1)

```
/**
 * @param {string} s
 * @return {number}
 */
var minAddToMakeValid = function(s) {
    if(s == "") return 0;

    // let stack = [];
    let open = 0, close = 0;

    for(let i = 0; i < s.length; i++){
        if(s[i] == "(") {
            open++;
        } else {
            if(open) {
                open--
            } else {
                close++;
            }
        }
    }

    return open + close;
};
```

***

## 4. 394. Decode String

### Time Everything is O(N) and Space Complexity O(N)

```
/**
 * @param {string} s
 * @return {string}
 */
var decodeString = function (s) {
    let stack = [];

    for (let i = 0; i < s.length; i++) {
        let char = s[i];
        if (char != "]") {
            stack.push(char);
            continue;
        }
        let cur = stack.pop();
        let str = "";

        while (cur !== "[") {
            str = cur + str;
            cur = stack.pop();
        }

        let num = "";
        cur = stack.pop();

        while (!isNaN(Number(cur))) {
            num = cur + num;
            cur = stack.pop();
        }
        stack.push(cur);
        stack.push(str.repeat(Number(num)));
    }

    return stack.join("");
};
```

***


## 5. 735. Asteroid Collision
### Time Everything is O(N) and Space Complexity O(N)


```
/**
 * @param {number[]} asteroids
 * @return {number[]}
 */
var asteroidCollision = function(asteroids) {
    let stack = [];

    for (let a of asteroids){
        while(stack.length && a < 0 && stack[stack.length - 1] > 0 ){
            let diff = a + stack[stack.length - 1];
            if(diff < 0) {
                stack.pop();
            } else if (diff  > 0){
                a = 0;
            } else {
                a = 0;
                stack.pop();
            }
        }

        if(a) { stack.push(a)}
    }

    return stack;
};
```

### Vide Reference 

[![YT Video](https://img.youtube.com/vi/LN7KjRszjk4/0.jpg)](https://www.youtube.com/watch?v=LN7KjRszjk4)

***

## 6. 456. 132 Pattern
### Time Everything is O(N) and Space Complexity O(N)

```
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var find132pattern = function (nums) {

    if(nums.length < 3) return false;

    let stack = [], min = Number.MIN_SAFE_INTEGER;

    for(let i = nums.length - 1; i >=0; i--){
        if(nums[i] < min) return true;

        while(stack.length && stack[stack.length - 1] < nums[i]){
            min = stack.pop();
        }

        stack.push(nums[i]);
    }
    return false;

};
```

***
