
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

### 1818. Minimum Absolute Sum Difference

Time Complexity: O(N Log N) // Due to Sorting
Space: O(N) // Due to DiffArr Storing all difference values

```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var minAbsoluteSumDiff = function (nums1, nums2) {

    let sum = 0;
    let diffArr = [];
    const MOD = Math.pow(10, 9) + 7;

    for (let i = 0; i < nums1.length; i++) {
        let diff = Math.abs(nums1[i] - nums2[i]);
        diffArr.push(diff);
        sum += diff; // sum all the absolute difference 
    }

    nums1.sort((a, b) => a - b);

    let minDiff = sum;

    for (let i = 0; i < nums1.length; i++) {
        let orgiDiff = diffArr[i];

        let left = 0, right = nums1.length - 1;
        let bestDiff = orgiDiff;

        while (left <= right) {
            let mid = Math.floor(left + (right - left) / 2);

            let diff = (nums1[mid] - nums2[i]);
            let absDiff = Math.abs(diff);

            if (absDiff < bestDiff) {
                bestDiff = absDiff;

                if (bestDiff == 0) break;
            }

            if (diff < 0) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        let replacedDiffSum = (sum - orgiDiff) + bestDiff;

        minDiff = Math.min(minDiff, replacedDiffSum);
    }

    return minDiff % MOD;

};

```

***









## Hard
