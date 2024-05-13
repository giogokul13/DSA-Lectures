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
