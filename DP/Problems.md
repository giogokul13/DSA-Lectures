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

### 64. Minimum Path Sum

<img width="385" alt="image" src="https://github.com/user-attachments/assets/6d98b24b-614b-4a0e-8702-39bb17d3ad2d">

```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function (grid) {
    let rows = grid.length;
    let cols = grid[0].length;

    let dp = Array.from({ length: rows }, () => new Array(cols).fill(0));

    dp[0][0] = grid[0][0];

    for (let j = 1; j < cols; j++) {
        dp[0][j] = dp[0][j - 1] + grid[0][j];
    }
    console.log("Pass 1", dp);

    for (let i = 1; i < rows; i++) {
        dp[i][0] = dp[i - 1][0] + grid[i][0];
    }

    console.log("Pass 1", dp);

    for (let i = 1; i < rows; i++) {
        for (let j = 1; j < cols; j++) {
            dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
        }
    }
    console.log("Final", dp);

    return dp[rows - 1][cols - 1];
};
```

The time complexity of this solution is O(m*n), where m is the number of rows and n is the number of columns in the grid. This is because we iterate through each cell in the grid exactly once to calculate the minimum path sum.

The space complexity is also O(m*n) because we are using a 2D array of the same size as the input grid to store the minimum path sum values for each cell.
 
***

### 198. House Robber

<img width="383" alt="image" src="https://github.com/user-attachments/assets/8dbffc44-9612-4250-b23a-7cb758f96642">

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
    if(nums.length == 0) return 0;

    if(nums.length == 1) return nums[0];


    let dp = new Array(nums.length).fill(0);
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]); 

    for(let i = 2; i < nums.length; i++) {
        dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
    }

    return dp[nums.length - 1];
};
```
Time and Space are O(N)
***

### 213. House Robber II

<img width="383" alt="image" src="https://github.com/user-attachments/assets/346b8315-2438-4414-84c8-f02e47e6f16d">

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
    if (nums.length == 0) return 0;

    if (nums.length == 1) return nums[0];

    if (nums.length == 2) return Math.max(nums[0], nums[1]);
    if (nums.length == 3) return Math.max(nums[0], nums[1], nums[2]);

    let case1 = robMoney(nums.slice(0, nums.length - 1));
    let case2 = robMoney(nums.slice(1));

    return Math.max(case1, case2);

};

function robMoney(nums) {
    if (nums.length === 0) return 0;
    if (nums.length === 1) return nums[0];
    
    let prev1 = Math.max(nums[0], nums[1]); // dp[i-1]
    let prev2 = nums[0];                     // dp[i-2]
    
    for (let i = 2; i < nums.length; i++) {
        let current = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = current;
    }
    
    return prev1;
}
```
Time and Space O(1)

***






























## Hard
