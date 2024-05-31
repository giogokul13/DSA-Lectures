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

## 7. 622. Design Circular Queue
### Time Everything is O(1) and Space Complexity O(N)

```
/**
 * @param {number} k
 */
var MyCircularQueue = function (k) {
    this.queue = new Array(k);
    this.front = 0;
    this.rear = 0;
    this.size = 0;
    this.length = k;
};

/** 
 * @param {number} value
 * @return {boolean}
 */
MyCircularQueue.prototype.enQueue = function (value) {
    if (this.isFull()) return false;

    this.size++;
    this.queue[this.rear] = value;
    this.rear = (this.rear + 1) % this.length;

    return true;
};

/**
 * @return {boolean}
 */
MyCircularQueue.prototype.deQueue = function () {
    if (this.isEmpty()) return false;

    this.size--;
    this.front = (this.front + 1) % this.length;

    return true;
};

/**
 * @return {number}
 */
MyCircularQueue.prototype.Front = function () {
    if(this.isEmpty()) return -1;
    
    return this.queue[this.front];
};

/**
 * @return {number}
 */
MyCircularQueue.prototype.Rear = function () {
    if(this.isEmpty()) return -1;

    let index = (this.rear + this.length - 1) % this.length;
    
    return this.queue[index];
};

/**
 * @return {boolean}
 */
MyCircularQueue.prototype.isEmpty = function () {
    return (this.size == 0);
};

/**
 * @return {boolean}
 */
MyCircularQueue.prototype.isFull = function () {
    return this.size == this.length;
};

/** 
 * Your MyCircularQueue object will be instantiated and called as such:
 * var obj = new MyCircularQueue(k)
 * var param_1 = obj.enQueue(value)
 * var param_2 = obj.deQueue()
 * var param_3 = obj.Front()
 * var param_4 = obj.Rear()
 * var param_5 = obj.isEmpty()
 * var param_6 = obj.isFull()
 */
```

***

## 8. 1673. Find the Most Competitive Subsequence
### Time O(N) and Space Complexity O(K)

```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var mostCompetitive = function(nums, k) {
    let remove = nums.length - k;
    let stack = [];

    for(let n of nums){
        while(stack.length && stack[stack.length - 1] > n && remove) {
            stack.pop();
            remove--
        }

        stack.push(n);
    }

    while(stack.length && remove) {
        stack.pop();
        remove--;
    }


    return stack;
};
```

***
## 9. 1670. Design Front Middle Back Queue

## Solution 1

The time complexity of the pushFront, pushMiddle, and pushBack methods is O(n) because in the worst case scenario, we may need to shift all elements in the queue to make space for the new element. The time complexity of popFront and popMiddle is also O(n) because in the worst case scenario, we may need to shift all elements in the queue after removing an element. The time complexity of popBack is O(1) because we are removing the last element in the queue.

The space complexity of the FrontMiddleBackQueue class is O(n) because we are storing n elements in the queue.

```

var FrontMiddleBackQueue = function () {
    this.queue = [];
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushFront = function (val) {
    this.queue.unshift(val);
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushMiddle = function (val) {

    let mid = Math.floor((this.queue.length) / 2);

    this.queue.splice(mid, 0, val);
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushBack = function (val) {
    this.queue.push(val);
};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popFront = function () {
    return (this.queue.length == 0) ? -1 : this.queue.shift();
};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popMiddle = function () {
    if (this.queue.length == 0) return -1

    let mid = Math.floor((this.queue.length - 1) / 2);
    return this.queue.splice(mid, 1)[0];

};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popBack = function () {
    return (this.queue.length == 0) ? -1 : this.queue.pop();
};

/** 
 * Your FrontMiddleBackQueue object will be instantiated and called as such:
 * var obj = new FrontMiddleBackQueue()
 * obj.pushFront(val)
 * obj.pushMiddle(val)
 * obj.pushBack(val)
 * var param_4 = obj.popFront()
 * var param_5 = obj.popMiddle()
 * var param_6 = obj.popBack()
 */
```

## Solution 2

// T.C: 
// O(1) for init and methods other than pushMiddle(), popMiddle()
// O(N) for pushMiddle(), popMiddle()
// S.C: O(N) for storage 

```


// Doubly linked list node
function ListNode(val, prev, next) {
    this.val = val || 0;
    this.prev = prev || null;
    this.next = next || null;
}

var FrontMiddleBackQueue = function() {
    this.head = null;
    this.tail = null;
    this.len = 0;
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushFront = function(val) {
    if (this.len === 0) {
        this.head = new ListNode(val);
        this.tail = this.head;
        this.len += 1;
        return;
    }
    
    let newNode = new ListNode(val);
    newNode.next = this.head;
    this.head.prev = newNode;
    this.head = newNode; // the new node becomes the new head
    this.len += 1;
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushMiddle = function(val) {
    if (this.len <= 1) {
        this.pushFront(val);
        return;
    }
    let cur = this.head;
    for (let i = 1; i < Math.floor(this.len / 2); i++) { // we go to previous node of median
        cur = cur.next;    
    }
    let newNode = new ListNode(val);
    let next = cur.next;
    cur.next = newNode;
    newNode.prev = cur;
    newNode.next = next;
    if (next) next.prev = newNode;
    this.len += 1;
};

/** 
 * @param {number} val
 * @return {void}
 */
FrontMiddleBackQueue.prototype.pushBack = function(val) {
    if (this.len === 0) {
        this.pushFront(val);
        return;
    }
    
    let newNode = new ListNode(val);
    this.tail.next = newNode;
    newNode.prev = this.tail;
    this.tail = newNode; // end node becomes the new tail
    this.len += 1;
};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popFront = function() {
    if (this.len === 0) {
        return -1;
    }
    let front = this.head;
    let next = front.next;
    if (next) next.prev = null;
    this.head = next;
    this.len -= 1;
    return front.val;
};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popMiddle = function() {
    if (this.len <= 2) {
        return this.popFront();
    }
    let cur = this.head;
    for (let i = 1; i < Math.ceil(this.len / 2); i++) { // we go to median node
        cur = cur.next;    
    }

    let prev = cur.prev;
    let next = cur.next;
    cur.prev = null;
    cur.next = null;
    if (prev) prev.next = next;    
    if (next) next.prev = prev;
    this.len -= 1;
    return cur.val;
};

/**
 * @return {number}
 */
FrontMiddleBackQueue.prototype.popBack = function() {
    if (this.len <= 1) {
        return this.popFront();
    }
    let end = this.tail;
    let prev = end.prev;
    end.prev = null;
    prev.next = null;
    this.tail = prev;
    this.len -= 1;
    return end.val;
};

/** 
 * Your FrontMiddleBackQueue object will be instantiated and called as such:
 * var obj = new FrontMiddleBackQueue()
 * obj.pushFront(val)
 * obj.pushMiddle(val)
 * obj.pushBack(val)
 * var param_4 = obj.popFront()
 * var param_5 = obj.popMiddle()
 * var param_6 = obj.popBack()
 */
```

***

## 10. 621. Task Scheduler
### Time O(N) and Space Complexity O(N)

```
/**
 * @param {character[]} tasks
 * @param {number} n
 * @return {number}
 */

var leastInterval = function(tasks, n) {
  // the map will be our tracking mechanism
  let m = new Map();
  
  // the max occurrences
  let maxVal = 0;
  
  // the number of tasks that has the max occurrences
  let maxValCount = 0;
  
  for(let k of tasks){
    let tVal = m.has(k) ? m.get(k)+1: 1;
    m.set(k, tVal);
	// set our maxVal and number of maxVal tasks only if we have a new max
    if(tVal > maxVal){
      maxVal = tVal;
      maxValCount = 1;
	// otherwise, increment number of maxVal tasks
    } else if(tVal === maxVal){
      maxValCount++;
    }
  }
  // our formula, handle the edge case
  return Math.max(tasks.length, (maxVal - 1) * (n + 1) + maxValCount);
};
```

***
