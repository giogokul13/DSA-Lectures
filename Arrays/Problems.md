
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










## Medium Problems

### 53. Maximum Subarray

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
