
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
