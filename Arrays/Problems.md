
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

