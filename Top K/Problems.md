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
