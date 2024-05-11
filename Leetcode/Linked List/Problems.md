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




    
