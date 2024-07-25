
## Easy Problem

### 121. Best Time to Buy and Sell Stock
Time Complexity = O(N) - Iterates through all the items in the input
Space Complexity - O(1) Constant, as there is no additional space used.

```
var maxProfit = function (prices) {

    let profit = 0;
    let previousDay = 0;
    let nextDay = 1;
    while (nextDay < prices.length) {
        if (prices[previousDay] < prices[nextDay]) {
            let cost = prices[nextDay] - prices[previousDay];
            profit = Math.max(profit, cost);
        } else {
            previousDay = nextDay // Move a head to next day 
        }

        nextDay++; //Move to the next day
    }

    return profit;

};
```

***

### 118. Pascal's Triangle

Time: O(N * N);
Space: O(N * N) // as we construct the triangle.

```
/**
 * @param {number} numRows
 * @return {number[][]}
 */

var generate = function (numRows) {
    let triangle = [[1]];

    if (numRows == 1) return triangle; // Base condition

    for (let i = 1; i < numRows; i++) { // Loop through the given no, of rows
        let arr = [];
        let tri = triangle[i - 1];
        for (let j = 0; j < tri.length + 1; j++) { // loop through eh previous rows length + 1, as a new element is going to be added
 
            arr[j] = (tri[j] || 0) + (tri[j - 1] || 0); // sum up the current posotion vaue and previous position value
        }

        triangle.push(arr);
    }

    return triangle;
};
```

***

### 88. Merge Sorted Array

Time: O(M + N);
Space: O(1)

```
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function (nums1, m, nums2, n) {
    let i = m - 1;
    let j = n - 1;
    let k = (m + n) - 1
    while (j >= 0) { // two pointer method
        if (i >= 0 && nums1[i] > nums2[j]) { // if the nums1 or nums2 is greater, then assigng the greater element to the Last cell 
            nums1[k] = nums1[i];
            i--;  // decrement nums1 and 
            k--; // decrement the overall length
        } else { 
            nums1[k] = nums2[j];
            k--;
            j--;
        }
    }
};
```

***

### 169. Majority Element

```
/**
 * @param {number[]} nums
 * @return {number}
 */
 /**
    The Boyer-Moore Voting Algorithm works by maintaining a balance of counts for the current candidate. 
    If the balance (majority) goes to zero, it means that the current candidate is not the majority element, 
    and a new candidate is chosen. This process continues until the end of the array, 
    and the candidate that remains is returned as the majority element
  */

var majorityElement = function(nums) {
    let res = 0;
    let majority = 0;
    
    for (let n of nums) {
        if (majority === 0) {
            res = n;
        }
        
        majority += (n === res) ? 1 : -1;
    }
    
    return res;    
};
```

***

### 1. Two Sum
Time - O(N) - Traversing through the Array items
Space - At worst case it is O(N) -  As we would be storing all the numbers.

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
    let indexMap = new Map();

    for (let i = 0; i < nums.length; i++) {
        let num = nums[i];
        if (indexMap.has(num)) return [i, indexMap.get(num)];

        let diff = target - num;
        indexMap.set(diff, i);
    }
};
```

***


### 18. 4Sum

Time Complexity - O(N ^ 3)
Space Complexity = O(1)

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var fourSum = function (nums, target) {
    nums.sort((a, b) => a - b)      //First sort the array in ascending order
    let len = nums.length;
    let left = 0, right = 0, sum = 0;
    let result = [];
    for (let i = 0; i < len - 3; i++) {
        for (let j = i + 1; j < len - 2; j++) {
            left = j + 1;
            right = len - 1;
            while (left < right) {
                sum = nums[i] + nums[j] + nums[left] + nums[right];
                if (sum === target) {
                    result.push([nums[i], nums[j], nums[left], nums[right]])
                    while (nums[left] === nums[left + 1]) left++;     //To avoid same values for left pointer
                    while (nums[right] === nums[right - 1]) right--;  //To avoid same values for right pointer
                    left++;
                    right--;
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
            while (nums[j] === nums[j + 1]) j++; // Avoid the same consecutive number in the sorted Array
        }
        while (nums[i] === nums[i + 1]) i++; // Avoid the same consecutive number in the sorted Array
    }
    return result;
};
```

*** 




























## Medium Problems

### 53. Maximum Subarray
### Kadane's Algorithm

TC- O(N);
Space: O(1)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
    if (nums.length == 0) return nums[0];
    let sum = nums[0];
    let max = sum;
    for (let i = 1; i < nums.length; i++) {
        if (sum < 0) {
            sum = nums[i];
        } else {
            sum += nums[i];
        }
        // sumArray.push(sum);
        if(max < sum) max = sum;
    }
    // console.log(sumArray);
    return max;
};
```

*** 


### 73. Set Matrix Zeroes
Time Complexity: O(n * N)
Space Complexity: O(1)

```
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function (matrix) {
    let m = matrix.length;
    let n = matrix[0].length;
    let colIndex = 1;

    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {

            if (matrix[i][j] == 0) {
                matrix[i][0] = 0; // mark the Row with Zero 

                if (j != 0) {
                    matrix[0][j] = 0;

                } else {
                    colIndex = 0;
                }
            }
        }
    }

    for (let i = 1; i < m; i++) { // Loop through the remaining elements
        for (let j = 1; j < n; j++) {

            if (matrix[i][j] !== 0) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
    }

    if (matrix[0][0] == 0) {
        for (let i = 0; i < n; i++) {
            matrix[0][i] = 0
        }
    }

    if (colIndex == 0) {
        for (let j = 0; j < m; j++) {
            matrix[j][0] = 0;
        }
    }
};
```

***

### 31. Next Permutation
Time Complexity: O(N)
Space Complexity: O(1) 
```
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function (nums) {

    let swap = function (i, j) { // swap the two given numbers in the nums array;
        [nums[i], nums[j]] = [nums[j], nums[i]];
    }

    let reverse = function (index) {
        let start = index, end = nums.length - 1;

        while (start < end) {
            swap(start, end);
            start++;
            end--;
        }
    }

    let getLarge = function (index) { //return the largest item index from the given Index;
        for (let n = nums.length - 1; n > index; n--) {
            if (nums[n] > nums[index]) return n;
        }
    }

    for (let n = nums.length - 1; n >= 0; n--) {
        if (nums[n] < nums[n + 1]) {
            let large = getLarge(n);
            swap(n, large);
            reverse(n + 1);
            return;
        }
    }

    nums.reverse();


};
```

***

### 48. Rotate Image

Time - O(N * N)
Space - O(1) 

```
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    
    //First Reverse the Array (rows) 1st Row to last row and last row to First row
    matrix.reverse();

    // Now swap the diagnal symmetric elements in the Array. 
    // this will replace the lower half of the array diagnally

    for(let i = 0; i < matrix.length; i++){
        for(let j = i + 1; j < matrix.length; j++){
            let temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
};               
```
Legendary Solution https://leetcode.com/problems/rotate-image/.

***


### 56. Merge Intervals


```
var merge = function (intervals) {
    let ans = [];

    // if once interval return as such
    if (intervals.length == 1) return intervals;

    intervals.sort((a, b) => a[0] - b[0]); // sort the interval by start

    let newInterval = intervals[0];
    ans.push(newInterval);
    for (let i = 0; i < intervals.length; i++) {
        let interval = intervals[i];
        // if the current Interval start is <= to previous interval then update the max end and continue
        if (interval[0] <= newInterval[1]) {
            newInterval[1] = Math.max(interval[1], newInterval[1]);
        } else { // else new interval.
            newInterval = interval;
            ans.push(interval);
        }
    }
    return ans;
};
```

***


### 287. Find the Duplicate Number
Time - O(N)
Space - O(1)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var findDuplicate = function (nums) {
    let map = new Map();

    for (let i = 0; i < nums.length; i++) {

        if (map.has(nums[i])) {
            return nums[i];
        }
        map.set(nums[i], 0);
    }

    return -1;
};

```

***


### 74. Search a 2D Matrix

Time: O(Log (M * N))
Space =  O(1)

```
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function (matrix, target) {
    let rowIndex = getPotentialRow(matrix, target);
    let isElementFound = false;
    if (rowIndex != -1) isElementFound = binarySearchOnRow(rowIndex, matrix, target);

    return isElementFound;

};

/**
    Function to indentify the row which has the potential value
 */
function getPotentialRow(matrix, target) {
    let start = 0;
    let end = matrix.length - 1;

    while (start <= end) {
        let mid = Math.floor(start + (end - start) / 2);

        if (matrix[mid][0] <= target && target <= matrix[mid][matrix[0].length - 1]) {
            return mid;
        }

        if (matrix[mid][0] < target) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }
    return -1
}

/**
    Function to perform the binary search on the idetified row
 */
function binarySearchOnRow(rowIndex, matrix, target) {
    let start = 0;
    let end = matrix[rowIndex].length - 1;
    while (start <= end) {
        let mid = Math.floor(start + (end - start) / 2);

        if (matrix[rowIndex][mid] == target) return true;

        if (matrix[rowIndex][mid] < target) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }

    return false;
}
```

*** 


### 50. Pow(x, n)
Time - O(log N) - Executing as we reduce the given N number
Space - O(log N) - Call Stack

The time complexity of this solution is O(log n) because we are dividing the problem size by half in each recursive call. 
The space complexity is also O(log n) because of the recursive calls on the call stack.

```
/**
 * @param {number} x
 * @param {number} n
 * @return {number}
 */
var myPow = function (x, n) {
    // return Math.pow(x, n);
    let mathPower = function (x, n) {
        if (x == 0) return 0; // Zero to he power anything is Zero 0 ^ 2 = 0

        if (n == 0) return 1; // anything to the power 0 is 1 2 ^ 0 = 1

        if (n < 0) {
            n = Math.abs(n);
            x = 1 / x;
        }

        if (n % 2 == 0) { // on even number
            let power = mathPower(x, Math.floor(n / 2));
            return power * power;
        } else { // on odd number n = n * n - 1 * n - 2
            return x * mathPower(x, n - 1);
        }

    }

    return mathPower(x, n);
};
```

*** 


### 229. Majority Element II

Time Complexity - O(N)
Space = O(1), as we know there is going to be at Maximum 2 elements anytime.

```
/**
    The Boyer-Moore Voting Algorithm
    The approach of taking only two elements is beacuse at max there can be only two elements picked 1/3 ratio
 */

var majorityElement = function (nums) {
    let [num1, num2] = [0, 0]; // these are majority Elements
    let [count1, count2] = [0, 0]; // counts defaulted to 0, 0

    for (let num of nums) {
        if (num == num1) { // if the match is found then increment the count
            count1++;
        } else if (num == num2) {
            count2++;
        } else if (count1 == 0) { // if first match then assign it as num and incremase the count
            num1 = num;
            count1++;
        } else if (count2 == 0) {
            num2 = num;
            count2++;
        } else { // else decrement the count when there is a non matching element found 
            count1--;
            count2--;
        }
    }

    [count1, count2] = [0, 0];

    for (let num of nums) { // check the count of the selected maximum numbers
        if (num == num1) {
            count1++;
        } else if (num == num2) {
            count2++;
        }
    }

    let result = [];

    // the the selected numbers count is greater then the  1/ 3rd of the Array size then add it to the list
    if (count1 > Math.floor(nums.length / 3)) {
        result.push(num1);
    }


    if (count2 > Math.floor(nums.length / 3)) {
        result.push(num2);
    }

    return result;
}
```

***

### 62. Unique Paths
Time and Space =  O(M * N)

```
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */

var uniquePaths = function(m, n){
    let grid = new Array(m).fill(0).map(() => Array(n).fill(0));

    for(let i = 0; i < m; i++){  //first column values to be 1
        grid[i][0] = 1;
    }

    for(let i = 0; i < n; i++){ // first row values to be 1
        grid[0][i] = 1;
    }


    for(let i = 1; i < m; i++){ 
        //loop through the grid and calculate the current value by the previous left cell and top cell
        for(let j = 1; j < n; j++){
            grid[i][j] = grid[i - 1][j] + grid[i][j - 1];
        }
    }


    return grid[m - 1][n - 1];
}
```

***

### 128. Longest Consecutive Sequence

```
/**
 * @param {number[]} nums
 * @return {number}
 */

//  Time : O(N Log N), Space: O(1)
var longestConsecutive = function (nums) {
    if (nums.length == 0) return 0;

    nums = nums.sort((a, b) => a - b);

    let maxLength = 1;
    let counter = 1;
    for (let i = 0; i < nums.length; i++) {

        if (nums[i] == nums[i + 1]) continue;

        if (nums[i] + 1 == nums[i + 1]) {
            counter++;
        } else {
            maxLength = Math.max(maxLength, counter)
            counter = 1;
        }
    }

    return maxLength;
}; 

/**
    Time is O(N), Space is O(N)
 */
var longestConsecutive = function (nums) {
    if (nums.length == 0) return 0;

    let set = new Set(nums);
    let longestSeq = 0;

    for (let num of nums) {
        if (!set.has(num - 1)) {
            let count = 0;
            while (set.has(num + count)) {
                count++;
            }

            longestSeq = Math.max(count, longestSeq);
        }
    }

    return longestSeq;
}
```

***

















## Hard 

### 493. Reverse Pairs

```

```

***
