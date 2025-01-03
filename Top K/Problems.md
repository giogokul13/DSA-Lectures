## Easy

1005. Maximize Sum Of Array After K Negations

<img width="419" alt="{F5BCC7D3-C973-4E9E-B453-1B754FC29053}" src="https://github.com/user-attachments/assets/ccaa04cc-4397-4081-a122-4d0310d0305d" />

```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var largestSumAfterKNegations = function (nums, k) {

    nums.sort((a, b) => a - b);
    for (let i = 0; i < nums.length && k > 0; i++) {
        if (nums[i] < 0) {
            nums[i] = -nums[i];
            k--;
        }
    }

    nums.sort((a, b) => a - b); // Re-sort after flipping negatives
    if (k % 2 === 1) {
        nums[0] = -nums[0];
    }

    return nums.reduce((sum, num) => sum + num, 0);
};
```
Time is O(N log N), Space O(N)
***


## Medium

347. Top K Frequent Elements
![{276A79E6-0D04-4B01-AE35-AC1356735792}](https://github.com/user-attachments/assets/9bc27b74-8b18-4139-ad03-2fa12822039b)

```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function (nums, k) {
    let holder = new Map();
    let result = [];
    for (let num of nums) {
        holder.set(num, (holder.get(num) || 0) + 1);
    }

    let buckets = new Array(nums.length + 1).fill(null).map(() => []);
    for (let [key, freq] of holder) {
        buckets[freq].push(key);
    }

    for (let i = buckets.length - 1; (i >= 0 && result.length < k); i--) {
        result.push(...buckets[i]);
    }

    return result;
};
```

***
