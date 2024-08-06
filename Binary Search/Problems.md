
# Problems

## Easy


## Medium

### 540. Single Element in a Sorted Array

Time: O(log N)
Space: O(1)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNonDuplicate = function(nums) {
    let start = 0;
    let end = nums.length - 1;

    while(start <= end){

        if(nums[start] == nums[start + 1]){
            start += 2;
        } else {
            return nums[start];
        }
    }

    return -1;
};

```

***

## Hard
