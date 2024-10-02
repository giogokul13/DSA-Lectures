# Dynamic Programmig Problems

## Easy 




## Medium

### 152. Maximum Product Subarray

<img width="381" alt="image" src="https://github.com/user-attachments/assets/c8d5355c-dc21-4bd3-acf2-70c85b940bfd">

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function (nums) {
    if (nums.length === 0) return 0;

    let maxProd = nums[0]; 
    let minProd = nums[0]; 
    let result = nums[0];

    for (let i = 1; i < nums.length; i++) {

        if(nums[i] < 0) {
            [maxProd, minProd] = [minProd, maxProd];
        }

        maxProd = Math.max(nums[i], maxProd * nums[i]);
        minProd = Math.min(nums[i], minProd * nums[i]);

        result = Math.max(result, maxProd);
    }

    return result;
};
```
Time and Space is O(N and O(1))
***

### 300. Longest Increasing Subsequence

<img width="381" alt="image" src="https://github.com/user-attachments/assets/88e0d29b-6986-4a1e-bd99-1cb0fae98f19">

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {
    let tails = [];

    for(let num of nums) {
        let left = 0, right = tails.length;

        while(left < right) {
            let mid = Math.floor((left + right) / 2);
            if(tails[mid] < num){
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        if(left < tails.length) {
            tails[left] = num;
        } else {
            tails.push(num);
        }
    }

    return tails.length;
};
```
Time O9N loh N0
Space O(N)
***

### 

<img width="382" alt="image" src="https://github.com/user-attachments/assets/c8db65c5-075b-4142-b6af-c2c6d2f152e2">

```
/**
 * @param {string} text1
 * @param {string} text2
 * @return {number}
 */
var longestCommonSubsequence = function (text1, text2) {
    let m = text1.length;
    let n = text2.length;

    // Create a 2D array to store the lengths of the longest common subsequence
    let dp = new Array(m + 1).fill(0).map(() => new Array(n + 1).fill(0));

    // Fill the dp array
    for (let i = 1; i <= m; i++) {
        for (let j = 1; j <= n; j++) {
            if (text1[i - 1] === text2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1; // Match found, extend the LCS
            } else {
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]); // Take the maximum LCS excluding one character
            }
        }
    }
    // console.log(dp);
    // The LCS length is in the bottom-right corner of the dp array
    return dp[m][n];
};

```
The time complexity of this solution is O(m*n), where m is the length of text1 and n is the length of text2. This is because we are filling up a 2D array of size (m+1) x (n+1) to store the lengths of the longest common subsequence, and we iterate through each cell of the array once.

The space complexity of this solution is also O(m*n) because we are using a 2D array of size (m+1) x (n+1) to store the lengths of the longest common subsequence.

***

### 72. Edit Distance

<img width="387" alt="image" src="https://github.com/user-attachments/assets/1f0d10ab-f117-4783-beed-c9d967c4c6a5">

```
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(word1, word2) {
    let m = word1.length;
    let n = word2.length;

    let dp = new Array(m + 1).fill(null).map(() => new Array(n + 1).fill(null));
    console.log(dp);

    for(let i = 0; i <= m; i++) {
        dp[i][0] = i;
    }

    for(let i = 0; i <= n; i++) {
        dp[0][i] = i;
    }

    for(let i = 1; i <= m; i++) {
        for(let j = 1; j <= n; j++) {
            if(word1[i - 1] == word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1;
            }
        }
    }

    console.log(dp);

    return dp[m][n];
};
```
Time and Space O(N * N) 

***
























## Hard



## Hard
