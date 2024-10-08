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

### 225. Implement Stack using Queues

```

var MyStack = function() {
    this.queue = [];
};

/** 
 * @param {number} x
 * @return {void}
 */
MyStack.prototype.push = function(x) {
    this.queue.push(x);
    for(let i = 0; i < this.queue.length - 1; i++){
        this.queue.push(this.queue.shift()) // remove the elements from first and then push it to the Array so that stack structure is formed
    }
};

/**
 * @return {number}
 */
MyStack.prototype.pop = function() {
    return this.queue.shift();
};

/**
 * @return {number}
 */
MyStack.prototype.top = function() {
    return this.queue[0];
};

/**
 * @return {boolean}
 */
MyStack.prototype.empty = function() {
    return this.queue.length == 0;
};

/** 
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
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
## Video referring : [https://www.youtube.com/watch?v=l6-y7MrHLB8[s](url)](url)

***

### 146. LRU Cache

Time : O(1)
Space O(N) - as we hae the cache being stored.

```

/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
    this.capacity = capacity;
    this.cache = new Map(); // Maintains the order of insertion
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
    if (!this.cache.has(key)) {
        return -1; // Key not found
    }
    
    const value = this.cache.get(key);
    this.cache.delete(key); // Remove the item
    this.cache.set(key, value); // Reinsert the item to mark it as recently used
    return value;
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
    if (this.cache.has(key)) {
        this.cache.delete(key); // Remove the old item
    }
    this.cache.set(key, value); // Insert the new item

    if (this.cache.size > this.capacity) {
        const firstKey = this.cache.keys().next().value; // Get the first (least recently used) item
        this.cache.delete(firstKey); // Remove it to maintain capacity
    }
};

/** 
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */

let map = new Map();
map.set(1, 11);
map.set(2, 22);
map.set(3, 33);

map.keys() // returns a iterrator
map.keys().next // provides {value: "key value", done: "true/false"};

```
***

### 994. Rotting Oranges

Time: M * N
Space: M * N

```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function (grid) {
    let queue = [];
    let time = 0, freshOranges = 0;
    let rows = grid.length;
    let cols = grid[0].length;

    // Count the no, of fresh oranges and push the rotten oranges
    for (let row = 0; row < rows; row++) { //m * n
        for (let col = 0; col < cols; col++) {
            if (grid[row][col] == 1) freshOranges++;
            if (grid[row][col] == 2) {
                queue.push([row, col]);
            }
        }
    }

    let directions = [[0, 1], [0, -1], [1, 0], [-1, 0]];// look at all the directions 4 sides and make the oranges rotten to make the identify the time  
    while (queue.length && freshOranges > 0) {
        let newQueue = [];
        while (queue.length) {
            let [r, c] = queue.shift();

            for (let dir of directions) {
                let [row, col] = [dir[0] + r, dir[1] + c];
                // on end bounds and when not a fresh orange continue
                if (row < 0 || row == rows || col < 0 || col == cols || grid[row][col] != 1) continue;

                grid[row][col] = 2;
                newQueue.push([row, col]);
                freshOranges-- // For Every rotten orange reduce fresh orange
            }
        }
        time++;
        queue = newQueue; // now assign the new rotten 
    }

    return (freshOranges == 0) ? time : -1;
};

```
***

### 901. Online Stock Span

Time and Space Complexity - O(N)

```
var StockSpanner = function() {
     this.stack = [];
};

/** 
 * @param {number} price
 * @return {number}
 */
StockSpanner.prototype.next = function(price) {
    this.stack.push(price);
    let days = 0;
    for(let i = this.stack.length - 1; i >= 0; i--){
        if(this.stack[i] > price ) break;
        days++;
    }
    return days;
};

/** 
 * Your StockSpanner object will be instantiated and called as such:
 * var obj = new StockSpanner()
 * var param_1 = obj.next(price)
 */
```

***




## Hard

### 460. LFU Cache

```
/**
 * @param {number} capacity
 */
var LFUCache = function (capacity) {
    this.capacity = capacity;
    this.cache = new Map(); // Stores key-value pairs
    this.freqMap = new Map(); // Stores key-frequency pairs
    this.freqList = new Map(); // Stores frequency-ordered sets of keys
    this.minFreq = 0;
};

/** 
 * @param {number} key
 * @return {number}
 */
LFUCache.prototype.get = function (key) {
    console.log("map ", this.freqMap);
    console.log("List ", this.freqList);
    if (!this.cache.has(key)) {
        return -1;
    }

    let value = this.cache.get(key);
    this.updateFrequency(key);

    return value;
};

/**
    Update Frequency in map and set
 */
LFUCache.prototype.updateFrequency = function (key) {
    let freq = this.freqMap.get(key);
    this.freqMap.set(key, freq + 1);

    this.freqList.get(freq).delete(key);
    if (this.freqList.get(freq).size === 0) {
        this.freqList.delete(freq);
        if (this.minFreq === freq) {
            this.minFreq++;
        }
    }

    if (!this.freqList.has(freq + 1)) {
        this.freqList.set(freq + 1, new Set());
    }
    
    this.freqList.get(freq + 1).add(key);
}

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LFUCache.prototype.put = function (key, value) {
    if (this.capacity === 0) return;

    if (this.cache.has(key)) {
        this.cache.set(key, value);
        this.updateFrequency(key);
        return;
    }

    if (this.cache.size >= this.capacity) {
        this.evictLFU();
    }

    this.cache.set(key, value);
    this.freqMap.set(key, 1);
    if (!this.freqList.has(1)) {
        this.freqList.set(1, new Set());
    }
    this.freqList.get(1).add(key);
    this.minFreq = 1;
};

/**
    Delete the least frequently used cache item.
 */
LFUCache.prototype.evictLFU = function () {
    let keys = this.freqList.get(this.minFreq);
    let evictKey = keys.keys().next().value;
    keys.delete(evictKey);

    if (keys.size === 0) {
        this.freqList.delete(this.minFreq);
    }

    this.cache.delete(evictKey);
    this.freqMap.delete(evictKey);
}

/** 
 * Your LFUCache object will be instantiated and called as such:
 * var obj = new LFUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
```

***

### 84. Largest Rectangle in Histogram

The time complexity of this algorithm is O(n) where n is the number of elements in the input array 'heights'. This is because we iterate through each element in the array once and perform constant time operations within the loop.

The space complexity of this algorithm is O(n) as well. This is because we use a stack data structure to keep track of indices of elements in the input array. In the worst case scenario, the stack could contain all elements of the input array, leading to O(n) space complexity.

```
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function (heights) {

    if (heights.length == 0) return 0;

    if (heights.length == 1) return heights[0];


    let max = 0, stack = [-1];
    for (let i = 0; i < heights.length; i++) {
        while (stack[stack.length - 1] !== -1 && heights[i] <= heights[stack[stack.length - 1]]) {
            let height = heights[stack.pop()];
            let width = i - stack[stack.length - 1] - 1;
            max = Math.max(max, height * width);
        }

        stack.push(i);
    }

    while (stack[stack.length - 1] !== -1) {
        let height = heights[stack.pop()];
        let width = heights.length - stack[stack.length - 1] - 1;
        max = Math.max(max, height * width);
    }

    return max;
};

```

***


### 239. Sliding Window Maximum

The time complexity of this solution is O(n) because we iterate through the input array nums once. The space complexity is O(n) because we use a deque data structure to store indices of potential maximum elements in the window, which can grow up to the size of the input array.

The reason for the time complexity being O(n) is that for each element in the input array, we perform constant time operations to update the deque and calculate the maximum element in the current window. The space complexity is O(n) because in the worst case scenario, the deque can store all elements of the input array.


```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSlidingWindow = function (nums, k) {
    if (nums.length === 0 || k === 0) return [];

    let result = [];
    let deque = []; // Stores indices of potential max elements in the window

    for (let i = 0; i < nums.length; i++) {
        // Remove elements from the front of the deque if they are out of the current window
        if (deque.length && deque[0] < i - k + 1) {
            deque.shift();
        }

        // Remove elements from the back of the deque if they are smaller than the current element
        // (since they can't be the maximum for the current or any future window)
        while (deque.length && nums[deque[deque.length - 1]] <= nums[i]) {
            deque.pop();
        }

        deque.push(i);

        // If we've processed at least k elements, add the current maximum to the result array
        if (i >= k - 1) {
            result.push(nums[deque[0]]);
        }
    }

    return result;
};

```

***
