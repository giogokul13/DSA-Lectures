# Leetcode Problems

#Easy

### 1.  1290 - Convert Binary Number in a Linked List to Integer

    ```/**
     * Definition for singly-linked list.
     * function ListNode(val, next) {
     *     this.val = (val===undefined ? 0 : val)
     *     this.next = (next===undefined ? null : next)
     * }
     */
    /**
     * @param {ListNode} head
     * @return {number}
     */
    var getDecimalValue = function (head) {
        let sum = 0;
        while (head != null) {
            sum = sum * 2 + head.val;  // sum * 2 will do a left shift for the operator
            head = head.next;
        }
    
        return sum;
    }; ```

---

### 2.  206. Reverse Linked List
### In Both Recursive and Iterative way
```
    /**
     * @param {ListNode} head
     * @return {ListNode}
     */
     // Iterative way
    var reverseList = function(head) {
        let curr = head;
        let prev = null;
    
        while(curr){
            let next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
    
        head = prev;
    
        return head;
    };
    
    // Recursive Way
    var reverseList = function(head, prev = null) {
    
       if(!head) return prev;
       let next = head.next;
    
       head.next = prev;
       return reverseList(next, head);
    };
```

---

### 3.  876. Middle of the LinkedList

```
    /**
     * Definition for singly-linked list.
     * function ListNode(val, next) {
     *     this.val = (val===undefined ? 0 : val)
     *     this.next = (next===undefined ? null : next)
     * }
     */
    /**
     * @param {ListNode} head
     * @return {ListNode}
     */
    
     /** Hair and tortoise Method with two pointers */
    var middleNode = function(head) {
        let slow = head;
        let fast = head;
    
        while(fast != null && fast.next != null){
            slow = slow.next; // move the slow node by one
            fast = fast.next.next; // move the dfat node by two;
        }
    
        return slow;
    
    };
```

### Video reference 
[![YT Video](https://img.youtube.com/vi/IPaMfcxQtP0/0.jpg)](https://www.youtube.com/watch?v=IPaMfcxQtP0)

***

### 4. 21. Merge Two Sorted Lists
Compare two elements from the list and insert the smallest at the new List create
```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
   var mergedList = {val: -1, next: null};
   let crt = mergedList;

   while(list1 && list2){
    if(list1.val > list2.val){
        crt.next = list2;
        list2 = list2.next;
    } else {
        crt.next = list1;
        list1 = list1.next;
    }
    crt = crt.next;
   }

   crt.next = list1 || list2;

   return mergedList.next;
};

```
### Another method to solve the problem

```
var mergeTwoLists = function (l1, l2) {
    if (!l1) return l2;
    else if (!l2) return l1;
    else if (l1.val <= l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2
    }
};
```
## Video Reference
[![YT Video](https://img.youtube.com/vi/0ougDTvVOFI/0.jpg)](https://www.youtube.com/watch?v=0ougDTvVOFI)

***

### 5. 237. Delete Node in a Linked List

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} node
 * @return {void} Do not return anything, modify node in-place instead.
 */
var deleteNode = function(node) {
    node.val = node.next.val; // pointing the next value at the current node
    node.next = node.next.next; // poniting the next node in the current node so that the current node is removed with its value and next node reference
};

```

### Video Reference

[![YT Video](https://img.youtube.com/vi/icnp4FJdZ_c/0.jpg)](https://www.youtube.com/watch?v=icnp4FJdZ_c)

***

### 6. 234. Palindrome Linked List
### Time O(n) Space O(n)
```
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(head) {
    let stack = [];

    while(head){ // loop through all the elements in the List and store it in the stack.
        stack.push(head.val);
        head = head.next;
    }

    let i = 0;
    let j = stack.length - 1;

    while( i < j){ // use a two pointer method to check the first and last element; if match continue checking else return false;
        if(stack[i] != stack[j]) return false;

        i++;
        j--;
    }

    return true;
};
```
### Optimized Time O(n) Space - O(1)
```
        class ListNode {
        constructor(val, next = null) {
            this.val = val;
            this.next = next;
        }
        }
        
        var isPalindrome = function(head) {
        if (!head || !head.next) {
            return true; // Empty list or single node is considered a palindrome
        }
        
        // Find the middle of the linked list using slow and fast pointers
        let slow = head;
        let fast = head;
        while (fast && fast.next) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // Reverse the second half of the linked list
        let prev = null;
        let curr = slow;
        while (curr) {
            let nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        
        // Compare the reversed second half with the first half
        let p1 = head;
        let p2 = prev;
        while (p2) {
            if (p1.val !== p2.val) {
                return false; // Not a palindrome
            }
            p1 = p1.next;
            p2 = p2.next;
        }
        
        return true; // Palindrome
        };
```
***

### 7. 160. Intersection of Two Linked Lists
### Time O(M + N) and Space = O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
// Time O(M + N) and Space = O(1)
// Loop through all the elements in the list and merge them
// if A is ended assign B
// If B is ended assign A
// when there is a match found then return it else null
var getIntersectionNode = function (headA, headB) {
    let a = headA, b = headB;
    while(a !== b){
        a = a ? a.next : headB;
        b = b ? b.next : headA;
    }

    return a;

};
```
***

### 8.  141. Linked List Cycle
### Time O(n) Space Constant O(1)

```
/**
 * @param {ListNode} head
 * @return {boolean}
 */ Time O(n) Space Constant O(1)

// hare and Tortoise approach
// hare move two times
// Tortoise move only once
// If there is a Cycle then there should be a match else we would reach the end.
var hasCycle = function(head) {
    let fast = head;
    let slow = head;
    while(fast && fast.next){
        fast = fast.next.next;
        slow = slow.next;

        if(fast == slow) return true;
    }

    return false;
};
```
***

### 9. 83. Remove Duplicates from Sorted List
## Time  O(n) and Space O(1)

```
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteDuplicates = function (head) {
    let curr = head;

    while (curr) {
        if (curr.next && curr.val == curr.next.val) {
            curr.next = curr.next.next;
        } else {
            curr = curr.next;
        }
    }

    return head;
};
```
***

### 10.  203. Remove Linked List Elements
## Time  O(n) and Space O(1)

```
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
    if(!head) return head;

    let curr = head.next;
    let prev = head;

    while(curr){
        if(curr.val == val){
            curr = curr.next;
            prev.next = curr;
        } else {
            prev = curr;
            curr = curr.next
        }
    }

    if(head.val == val) return head.next;

    return head;
};
```
***

# Medium Level Problems

## 1. 355. Design Twitter
### More of a Low Level Design

```
var Twitter = function () {
    this.tweetStore = {};
    this.followersMap = {};
    this.tweetTimeMap = {};
    this.time = 0;
};

/** 
 * @param {number} userId 
 * @param {number} tweetId
 * @return {void}
 */

Twitter.prototype.postTweet = function (userId, tweetId) {
    if (!this.tweetStore[userId]) this.tweetStore[userId] = [];
    this.tweetStore[userId].push(tweetId);
    this.tweetTimeMap[tweetId] = this.time++;
};

/** 
 * @param {number} userId
 * @return {number[]}
 */
Twitter.prototype.getNewsFeed = function (userId) {
    let tweets = [];
    if (this.tweetStore[userId]) {
        tweets = tweets.concat(this.tweetStore[userId]);
    }
    for (let followee of (this.followersMap[userId] || [])) {
        if (followee !== userId && this.tweetStore[followee]) {
            tweets = tweets.concat(this.tweetStore[followee]);
        }
    }
    const that = this;
    return tweets.sort((a, b) => that.tweetTimeMap[b] - that.tweetTimeMap[a]).slice(0, 10);
};

/** 
 * @param {number} followerId 
 * @param {number} followeeId
 * @return {void}
 */
Twitter.prototype.follow = function (followerId, followeeId) {
    if (!this.followersMap[followerId]) this.followersMap[followerId] = [];
    if (!this.followersMap[followerId].includes(followeeId)) {
        this.followersMap[followerId].push(followeeId);
    }
};

/** 
 * @param {number} followerId 
 * @param {number} followeeId
 * @return {void}
 */
Twitter.prototype.unfollow = function (followerId, followeeId) {
    if (this.followersMap[followerId]) {
        const followeeIndex = this.followersMap[followerId].indexOf(followeeId);
        if (followeeIndex !== -1) {
            this.followersMap[followerId].splice(followeeIndex, 1);
        }
    }
};

// Usage
// const obj = new Twitter();
// obj.postTweet(userId, tweetId);
// const param_2 = obj.getNewsFeed(userId);
// obj.follow(followerId, followeeId);
// obj.unfollow(followerId, followeeId);

```
### "
The time and space complexity of the methods in the Twitter class are as follows:

1. postTweet:
   - Time complexity: O(1)
     The postTweet method simply adds the tweetId to the tweetStore for the given userId. Since adding an element to an array has a time complexity of O(1), this method has a constant time complexity.

   - Space complexity: O(n)
     The space complexity of the tweetStore will be O(n), where n is the total number of tweets posted by all users.

2. getNewsFeed:
   - Time complexity: O(1)
     The getNewsFeed method retrieves the last 10 tweets from the tweetStore for the given userId. Since slicing an array has a time complexity of O(1), this method also has a constant time complexity.

   - Space complexity: O(1)
     The space complexity of this method is also O(1) because it only returns the last 10 tweets.

3. follow:
   - Time complexity: O(1)
     The follow method adds the followeeId to the followersMap for the given followerId. Since adding an element to an array has a time complexity of O(1), this method has a constant time complexity.

   - Space complexity: O(n)
     The space complexity of the followersMap will be O(n), where n is the total number of followees for all users.

Overall, the time complexity of each method is O(1) and the space complexity depends on the total number of tweets and followees in the system.
"

***

## 2. 92. Reverse Linked List II

### Time O(n) and space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} left
 * @param {number} right
 * @return {ListNode}
 */
var reverseBetween = function (head, left, right) {


    if (!head || left === right) {
        return head;
    }

    let dummy = new ListNode(-1); // Dummy node to handle edge case of reversing from the first node
    dummy.next = head;
    let prev = dummy;

    for (let i = 1; i < left; i++) {
        prev = prev.next;
    }

    let curr = prev.next;


    for (let i = left; i < right; i++) {
        let nextNode = curr.next;
        curr.next = nextNode.next;
        nextNode.next = prev.next;
        prev.next = nextNode;
    }

    return dummy.next;
};

```

***

## 3. 143. Reorder List
### Time O(n) and Space Complexity O(1)

### First we divide the list into two, reverse the second list.
### Use hare and tortose method to find the half of the list.

```
/**
 * @param {ListNode} head
 * @return {void} Do not return anything, modify head in-place instead.
 */
var reorderList = function (head) {
    let slow = head, fast = head.next;

    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }

    let second = slow.next // second array starting point

    let prev = null;
    slow.next = null;
    while (second) { // reverse the second half of the list
        let temp = second.next;
        second.next = prev;
        prev = second;
        second = temp;
    }

    //  Merge two lists / not two join the list

    second = prev;
    let first = head;

    while (second) { // replace the lists next pointers appropriately
        let [temp1, temp2] = [first.next, second.next];
        first.next = second;
        second.next = temp1;
        [first, second] = [temp1, temp2];
    }

    // Do not return as the question suggested.
};
```
### Video reference

[![YT Video](https://img.youtube.com/vi/S5bfdUTrKLM/0.jpg)](https://www.youtube.com/watch?v=S5bfdUTrKLM)

 ***


## 4. 19. Remove Nth Node From End of List

### Time O(n) and Space Complexity O(1)


```
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function(head, n) {
   let dummy = new ListNode(0);
   dummy.next = head;

    let first = dummy;
    let second = dummy;

    for(let i = 0; i <= n; i++){ // quickly move to n places on second loop
        second = second.next;
    }

    while(second){ // move untill the second is in last node , if second is in last noe the first is in the nth place.
        first = first.next;
        second = second.next;
    }

    first.next = first.next.next; // remove the node by connecting to the next.next node.

    return dummy.next // return the head as dummy.next = head;

};
```

***

## 5.  1721. Swapping Nodes in a Linked List

### Time O(n) and Space Complexity O(1)

```
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var swapNodes = function(head, k) {
    if(!head) return head;

    let length = 1;
    let [node, start] = [head, null];

    while(node){
        if(length == k) start = node;
        length++;
        node = node.next;
    }

    let end = head;

    for(let i = 1; i < length - k; i++ ){
        end = end.next;
    }

    [start.val, end.val] = [end.val,  start.val];

    return head;
};
```
### Video reference

[![YT Video](https://img.youtube.com/vi/KUTRaNOzmoo/0.jpg)](https://www.youtube.com/watch?v=KUTRaNOzmoo)
 
***

## 6. 2. Add Two Numbers

### Time O(max(m, n)) and Space Complexity O(max(m, n))

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function (l1, l2) {
    var list = new ListNode(0);
    let head = list;
    let sum = 0;
    let carry = 0;

    while (l1 || l2 || sum > 0) {
        if (l1) {
            console.log(l1.val);
            sum += l1.val;
            l1 = l1.next;
        }

        if (l2) {
            console.log(l2.val);
            sum += l2.val;
            l2 = l2.next;
        }

        if (sum > 9) {
            sum = sum - 10;
            carry = 1;
        }

        head.next = new ListNode(sum);
        head = head.next;

        [sum, carry] = [carry, 0] //set the sum to carry and carry to zero
    }

    return list.next;
};
```

***

## 7. 445. Add Two Numbers II

### Time O(max(m, n)) and Space Complexity O(max(m, n))

```
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function (l1, l2) {
    let stack1 = [];
    let stack2 = [];

    while (l1) {
        stack1.push(l1.val);
        l1 = l1.next;
    }

    while (l2) {
        stack2.push(l2.val);
        l2 = l2.next;
    }

    let l3 = new ListNode(0);

    while(stack1.length || stack2.length){
        let sum = 0;

        if(stack1.length) sum += stack1.pop();
        if(stack2.length) sum += stack2.pop();

        sum += l3.val;
        l3.val = sum % 10;
        let head = new ListNode(Math.floor(sum / 10));
        head.next = l3;
        l3 = head;
    }

    return (l3.val === 0) ? l3.next : l3;
};
```
### Video reference

[![YT Video](https://img.youtube.com/vi/Yc9buffV1G0/0.jpg)](https://www.youtube.com/watch?v=Yc9buffV1G0)

***

## 8. 142. Linked List Cycle II
### Time O(n) and Space Complexity O(1)

```
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function (head) {
    let fast = head;
    let slow = head;
    while (fast && fast.next) {
        fast = fast.next.next;
        slow = slow.next;

        if (fast == slow) {
            while (head != slow) {
                head = head.next;
                slow = slow.next;
            }

            return slow;
        }
    }

    fast = head;

    return null;
};
```

Video Reference 
[![YT Video](https://img.youtube.com/vi/95ZfuoSAUPI/0.jpg)](https://www.youtube.com/watch?v=95ZfuoSAUPI)


***

## 9. 430. Flatten a Multilevel Doubly Linked List
### Time O(n) and Space Complexity O(n)
Time -  as We loop through n nodes
Space - At worst case all nodes can have childrens.

```
/**
 * // Definition for a Node.
 * function Node(val,prev,next,child) {
 *    this.val = val;
 *    this.prev = prev;
 *    this.next = next;
 *    this.child = child;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var flatten = function (head) {
    let stack = [];
    let start = head;

    while (head) {
        if (head.child) {

            if (head.next) {
                stack.push(head.next);
            }

            head.next = head.child;
            head.next.prev = head;
            head.child = null;
        }

        if (!head.next && stack.length != 0) {
            head.next = stack.pop();
            head.next.prev = head;
        }

        head = head.next;
    }

    return start;
};
```

### Video Reference
[![YT Video](https://img.youtube.com/vi/t69HJbUugpQ/0.jpg)](https://www.youtube.com/watch?v=t69HJbUugpQ)


***

## 10. 61. Rotate List
### Time O(n) and Space Complexity O(1)

```
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function (head, k) {
    if (!head || !head.next) return head;
    let len = 1;
    let tail = head;

    while (tail.next) { // Get the length of the linked List
        tail = tail.next;
        len++;
    }

    tail.next = head;

    k = len - k % len;

    for (let i = 0; i < k; i++) {
        tail = tail.next;
        head = tail.next;
    }

    tail.next = null;
    return head;
};
```

***

## 11. 138. Copy List with Random Pointer
### Time O(n) and Space Complexity O(n)

```
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function (head) {
    if (!head) return null;

    let newListMap = new Map();

    let curr = head;
    while (curr) {
        newListMap.set(curr, new Node(curr.val));
        curr = curr.next;
    }

    curr = head;

    while (curr) {
        newListMap.get(curr).next = newListMap.get(curr.next) || null
        newListMap.get(curr).random = newListMap.get(curr.random) || null;
        curr = curr.next;
    }

    return newListMap.get(head);
};
```

***

## 12. 146. LRU Cache

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

```

***

## 13. 82. Remove Duplicates from Sorted List II
### Time O(n) and Space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteDuplicates = function (head) {
    let dummy = new ListNode(0, head);
    let prev = dummy;
    while (head) {
        if (head.next && head.val == head.next.val) {
            while (head.next && head.val == head.next.val) {
                head = head.next;
            }
            prev.next = head.next;
        } else {
            prev = prev.next;
        }

        head = head.next;
    }

    return dummy.next;
};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/R6-PnHODewY/0.jpg)](https://www.youtube.com/watch?v=R6-PnHODewY)

***

## 14. 86. Partition List
### Time O(n) and Space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} x
 * @return {ListNode}
 */
var partition = function (head, x) {
    let left = new ListNode(0);
    let right = new ListNode(0);
    let [leftTail, rightTail] = [left, right];

    while (head) {
        if (head.val < x) {
            leftTail.next = head;
            leftTail = leftTail.next;
        } else {
            rightTail.next = head;
            rightTail = rightTail.next;
        }

        head = head.next;
    }

    leftTail.next = right.next;
    rightTail.next = null;

    return left.next;
};

```
### Video Reference
[![YT Video](https://img.youtube.com/vi/KT1iUciJr4g/0.jpg)](https://www.youtube.com/watch?v=KT1iUciJr4g)

***

## 15. Find first node of loop in a linked list
### Time O(n) and Space Complexity O(1)
## Reference https://www.geeksforgeeks.org/find-first-node-of-loop-in-a-linked-list/
```
// Function to detect and remove loop
// in a linked list that may contain loop
function detectAndRemoveLoop(head)
{
    // If list is empty or has
  // only one node without loop
  if (head == null || head.next == null)
    return null;
 
  let slow = head, fast = head;
 
  // Move slow and fast 1
  // and 2 steps ahead
  // respectively.
  slow = slow.next;
  fast = fast.next.next;
 
  // Search for loop using
  // slow and fast pointers
  while (fast != null &&
         fast.next != null)
  {
    if (slow == fast)
      break;
    slow = slow.next;
    fast = fast.next.next;
  }
 
  // If loop does not exist
  if (slow != fast)
    return null;
 
  // If loop exists. Start slow from
  // head and fast from meeting point.
  slow = head;
  while (slow != fast)
  {
    slow = slow.next;
    fast = fast.next;
  }
 
  return slow;
}
```
*** 

## 16. 24. Swap Nodes in Pairs
### Time O(n) and Space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function(head) {
    let node = new ListNode(0);
    node.next = head;
    let curr = node;

    while(curr && curr.next && curr.next.next){
        let temp = curr.next;
        let temp2 = curr.next.next;
        curr.next = temp2;
        temp.next = temp2.next;
        temp2.next = temp;
        curr = curr.next.next;
    }

    return node.next;
};
```

[![YT Video](https://img.youtube.com/vi/o811TZLAWOo/0.jpg)](https://www.youtube.com/watch?v=o811TZLAWOo)

***

## 17. 1171. Remove Zero Sum Consecutive Nodes from Linked List
### Time O(n) and Space Complexity O(n) because we used Hash Map for space

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var removeZeroSumSublists = function(head) {
    let dummy = new ListNode();
    let cur = head;
    dummy.next = head;
    let m = new Map();
    m.set(0, dummy);
    let prefixSum = 0;
    while (cur !== null) {
        prefixSum += cur.val;
        if (m.has(prefixSum)) {
            // save pointer to next node
            let next = cur.next;

            // delete the nodes in between from map
            let temp = m.get(prefixSum).next;
            let tempPrefixSum = prefixSum;
            while (temp !== cur && temp !== null) {
                tempPrefixSum += temp.val;
                m.delete(tempPrefixSum);
                temp = temp.next;
            }

            // set a new cur
            cur = m.get(prefixSum);
            cur.next = next;
        } else {
            m.set(prefixSum, cur);
        }
        cur = cur.next;
    }
    
    return dummy.next;
};
```

***

## 18. 147. Insertion Sort List
### Time O(n ^ 2) and Space Complexity O(1) because we used Hash Map for space

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var insertionSortList = function (head) {

    if (!head) return head;

    let dummyNode = new ListNode(0, head);
    let curr = head.next;
    head.next = null;

    while (curr) {
        let prevNode = dummyNode;
        let nextNode = curr.next;

        while (prevNode.next && prevNode.next.val < curr.val) {
            prevNode = prevNode.next;
        }

        curr.next = prevNode.next;
        prevNode.next = curr;

        curr = nextNode;
    }

    return dummyNode.next;
};

```

***

## 19. 2074. Reverse Nodes in Even Length Groups
### Time O(n) and Space Complexity O(1) because we used Hash Map for space

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseEvenLengthGroups = function (head) {
    let dummyNode = new ListNode(0, head);
    let prev = dummyNode;
    let group = 0;
    while (prev.next) {
        group++;
        let values = [];
        // insert the group values inside the array
        let start = prev;
        for (let count = 0; count < group && start.next; count++) {
            start = start.next;
            values.push(start.val);
        }

        if (values.length % 2 == 0) {
            start = prev;
            for (let count = 0; count < group && start.next; count++) {
                start = start.next;
                start.val = values.pop();
            }
        }

        for (let count = 0; count < group && prev.next; count++) { // Navigate to the next nodes after performing the reverse
            prev = prev.next; 
        }
    }

    return dummyNode.next;
};
```

***

## 20. 382. Linked List Random Node
### Time O(n) and Space Complexity O(n) because we used Hash Map for space


```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 */
var Solution = function (head) {
    this.head = head;
    this.arr = [];
    let curr = head
    while(curr){
        this.arr.push(curr);
        curr = curr.next;
    }

    this.length = this.arr.length;
};

/**
 * @return {number}
 */
Solution.prototype.getRandom = function () {
   return this.arr[Math.floor(Math.random() * this.length)].val;
};
/** 
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(head)
 * var param_1 = obj.getRandom()
 */
```

***

## 21. 148. Sort List
### Solution 1
#### Time O(n log n) and Space Complexity O(n) because we used Array to store values


```
var sortList = function(head) {
    let arr = [];

    while(head){
        arr.push(head.val);
        head = head.next;
    }

    arr = arr.sort((a, b) => a - b); // Sort Array;
    let list = new ListNode();
    let dummy = list;
    for(let i = 0; i < arr.length; i++){
        let node = new ListNode(arr[i]);
        list.next = node;
        list = list.next;
    }

    return dummy.next;
};
```

### Solution 2 (Optimal)
### Time O(n log n) and Space Complexity O(1)

```
var sortList = function (head) {
    if (head === null || head.next == null) return head // check if list is empty or contains only one item.

    // Function is used to get the lenght of the Linkekd List
    let getLength = function (head) {
        let len = 0;
        let curr = head;
        while (curr) {
            len++;
            curr = curr.next
        }

        return len;
    }

    let split = function (head, steps) {
        if (!head) return null;

        for (let i = 1; (i < steps && head.next); i++) {
            head = head.next; // move right till the steps
        }

        let right = head.next;
        head.next = null;

        return right;
    }

    const merge = function (left, right, tail) {
        let curr = tail;
        while (left && right) {
            if (left.val < right.val) {
                curr.next = left;
                left = left.next;
            } else {
                curr.next = right;
                right = right.next;
            }
            curr = curr.next;
        }

        curr.next = left ? left : right;
        while (curr.next)
            curr = curr.next;

        return curr;
    };

    let length = getLength(head);
    let dummy = new ListNode(0);
    dummy.next = head;

    let steps = 1;

    while (steps < length) {
        let curr = dummy.next;
        let tail = dummy;

        while (curr) {
            const left = curr;
            const right = split(left, steps);
            curr = split(right, steps);

            tail = merge(left, right, tail);
        }

        steps *= 2;
    }

    return dummy.next;

}

```

***

## 22. 1669. Merge In Between Linked Lists
### Time O(m + n) and Space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {number} a
 * @param {number} b
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeInBetween = function(list1, a, b, list2) {
    let curr = list1;
    let i = 0;

    while( i < a -  1){
        curr = curr.next;
        i++;
    }

    head = curr;
    while(i <= b){
        i++;
        curr = curr.next;
    }
    head.next = list2;

    while(list2.next){
        list2 = list2.next;
    }

    list2.next = curr;

    return list1;
};
```
### Video Reference 

[![YT Video](https://img.youtube.com/vi/pI775VutBxg/0.jpg)](https://www.youtube.com/watch?v=pI775VutBxg)

***

## 23. 1472. Design Browser History

The time complexity for the `visit` method is O(1) because we are simply adding a new page to the array. 

The time complexity for the `back` and `forward` methods is also O(1) because we are accessing elements in the array based on the current index.

The space complexity for the `visit` method is O(n) where n is the number of pages visited so far. This is because we are storing all visited pages in an array.

Overall, the time complexity for all methods is O(1) and the space complexity is O(n).

```
/**
 * @param {string} homepage
 */
var BrowserHistory = function (homepage) {

    this.pages = [];
    this.pages.push(homepage);
    this.currentIndex = 0;
};

/** 
 * @param {string} url
 * @return {void}
 */
BrowserHistory.prototype.visit = function (url) {
    this.pages = this.pages.slice(0, this.currentIndex + 1);
    this.pages.push(url);
    this.currentIndex += 1;
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.back = function (steps) {
    this.currentIndex = this.pages[this.currentIndex - steps] ? this.currentIndex - steps : 0
    return this.pages[this.currentIndex];
};

/** 
 * @param {number} steps
 * @return {string}
 */
BrowserHistory.prototype.forward = function (steps) {
    this.currentIndex = this.pages[this.currentIndex + steps] ? this.currentIndex + steps : this.pages.length - 1
    return this.pages[this.currentIndex];
};

/** 
 * Your BrowserHistory object will be instantiated and called as such:
 * var obj = new BrowserHistory(homepage)
 * obj.visit(url)
 * var param_2 = obj.back(steps)
 * var param_3 = obj.forward(steps)
 */
```

*** 


## 24. 2095. Delete the Middle Node of a Linked List
### Time O(n) and Space Complexity O(1)

```

```
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteMiddle = function (head) {
    let dummy = new ListNode(0);
    dummy.next = head;
    let slow = dummy;
    let fast = head;
    while (fast && fast.next) {
        fast = fast.next.next;
        slow = slow.next;
    }

    slow.next = slow.next.next;

    return dummy.next;

};

***

## 25. 1019. Next Greater Node In Linked List
### Time O(n) and Space Complexity O(n)

```
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var nextLargerNodes = function (head) {
    let ans = [];
    let curr = head;
    let pointer = head;

    while (curr.next) {
        pointer = pointer.next;
        if (pointer.val > curr.val) {
            ans.push(pointer.val);
            curr = curr.next;
            pointer = curr;

        } else if (pointer.next == null) {
            ans.push(0);
            curr = curr.next;
            pointer = curr;
        }
    }

    ans.push(0);

    return ans;
};
```

***

## 26. 328. Odd Even Linked List
### Time O(n) and Space Complexity O(1)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var oddEvenList = function (head) {
    if(!head) return head;
    
    let odd = head;
    let even = head.next;

    let evenHead = even;

    while (even && even.next) {
        odd.next = odd.next.next;
        odd = odd.next;

        even.next = even.next.next;
        even = even.next;
    }

    odd.next = evenHead;

    return head;
};
```
### Vide Reference 

[![YT Video](https://img.youtube.com/vi/WoUAs7R3Ao4/0.jpg)](https://www.youtube.com/watch?v=WoUAs7R3Ao4)

***

## 27. 725. Split Linked List in Parts
### Time O(n) and Space Complexity O(1)

```

```

*** 
