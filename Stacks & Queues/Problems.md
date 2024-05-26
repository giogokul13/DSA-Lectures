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

## 2. 155. Min Stack
### Time  O(1) and Space Complexity O(N)

```

```

***

## Medium Problems

## 2. 155. Min Stack

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
