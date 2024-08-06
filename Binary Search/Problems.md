
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

 ### 33. Search in Rotated Sorted Array

Time O(Log N)
Space O(1)

 ```
 /**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {

    let start = 0;
    let end = nums.length - 1;

    while (start <= end) {
        let mid = Math.floor(start + (end - start) / 2);

        if (nums[mid] == target) {
            return mid;
        }

        if (nums[start] <= nums[mid]) {
            if (nums[start] <= target && target <= nums[mid]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        } else {
            if (nums[mid] < target && target <= nums[end]) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
    }

    return -1;
};

```
***




## Hard
