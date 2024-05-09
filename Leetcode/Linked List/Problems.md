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
[video](https://www.youtube.com/watch?v=IPaMfcxQtP0)




    
