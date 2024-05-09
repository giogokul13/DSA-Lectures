# Leetcode Problems

#Easy

### 1.  1290 - Convert Binary Number in a Linked List to Integer

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
     * @return {number}
     */
    var getDecimalValue = function (head) {
        let sum = 0;
        while (head != null) {
            sum = sum * 2 + head.val;  // sum * 2 will do a left shift for the operator
            head = head.next;
        }
    
        return sum;
    };


    
