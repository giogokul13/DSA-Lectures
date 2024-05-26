# Stacks and Queues

## Easy Problem

## 1. 496. Next Greater Element I
### Time O(M * N) and Space Complexity O(M)
### Solution 1
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

### Time O(M + N) and Space Complexity O(M)
### Solution 2
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

