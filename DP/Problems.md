# Dynamic Programmig Problems

## Easy 

### 455. Assign Cookies

<img width="419" alt="image" src="https://github.com/user-attachments/assets/a14f45cb-c25b-4e1e-9100-6d05a2b5c097">

```
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function (g, s) {
    let max = 0;
    let childIndex = 0;
    let cookieIndex = 0;

    g.sort((a, b) => b - a); // Sort the Childrens in decending order of greed
    s.sort((a, b) => b - a); // Sort the Cookies in decending order of Cookies count

    while (childIndex < g.length) {
        if (!g[childIndex] || !s[cookieIndex]) break;

        if (s[cookieIndex] >= g[childIndex]) { // now compare if the cookies is grater than greed, then incrementand move forward
            max++;
            cookieIndex++;
        }
        childIndex++;
    }
    return max;
};
```

Time O(N log N)
Space O(1)

***

### 119. Pascal's Triangle II

<img width="409" alt="image" src="https://github.com/user-attachments/assets/c2ef5478-dc85-41d0-be3d-789402011ad1">

```
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    let result = new Array(rowIndex + 1).fill(1);

    for(let i = 2; i <= rowIndex; i++) {
        for(let j = i - 1; j > 0; j--) {
            result[j] = result[j] + result[ j - 1]; 
        }
    }

    return result;
};
```
Time O(RowIndex * RowIndex)
Space O(rowIndex)

***

### 392. Is Subsequence

<img width="418" alt="image" src="https://github.com/user-attachments/assets/2b768f7e-628b-4c13-81e8-00d736551c3c">

```
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isSubsequence = function (s, t) {
    let i = 0; j = 0;

    while (i < s.length && j < t.length) {
        if (s[i] == t[j]) {
            i++;
        }
        j++;
    }
    return (i == s.length);
};
```
The time complexity of this solution is O(n), where n is the length of the longer string between s and t. This is because we iterate through both strings at most once.

The space complexity of this solution is O(1) because we are using a constant amount of extra space, regardless of the input size.

***

### 746. Min Cost Climbing Stairs

<img width="418" alt="image" src="https://github.com/user-attachments/assets/09f18391-24a1-4a09-b932-8e38a231d688">

```
/**
 * @param {number[]} cost
 * @return {number}
 */
var minCostClimbingStairs = function(cost) {
    let n = cost.length;
    let first = cost[0];
    let second = cost[1];

    if(n <= 2) return Math.min(first, second);

    for(let i = 2; i < n; i++) {
        let curr = cost[i] + Math.min(first, second);

        first = second;
        second = curr;
    }

    return Math.min(first, second);
};
```
Time O(N)
Space O(1)

***

### 1025. Divisor Game

<img width="412" alt="image" src="https://github.com/user-attachments/assets/f1ca03ba-6783-4053-bce7-f4bfb0002d70">

```
/**
 * @param {number} n
 * @return {boolean}
 */
var divisorGame = function(n) {
    return n % 2 == 0;
};
```
Time and Space is O(1)
***

### 1137. N-th Tribonacci Number

<img width="412" alt="image" src="https://github.com/user-attachments/assets/a0bb8af1-6af1-472b-8bbc-a1485841ec6c">

```
/**
 * @param {number} n
 * @return {number}
 */
var tribonacci = function (n) {
    if (n < 2) return n;

    let [first, second, third] = [0, 1, 1];
    let fourth = first + second + third;

    while (n > 2) {
        fourth = first + second + third;
        first = second;
        second = third;
        third = fourth;
        n--;
    }

    return third;
};
```
Time O(N)
Space O(1)
***

### 2900. Longest Unequal Adjacent Groups Subsequence I

<img width="420" alt="image" src="https://github.com/user-attachments/assets/6e0f9ac0-3582-4302-9479-c3a369fa5e40">

```
/**
 * @param {string[]} words
 * @param {number[]} groups
 * @return {string[]}
 */
var getLongestSubsequence = function(words, groups) {
    let ans = [];
    let flag = -1;

    for(let i = 0; i < groups.length; i++) {
        if(groups[i] != flag) {
            flag = groups[i];
            ans.push(words[i]);
        }
    }

    return ans;
};
```
Time and Space O(N)
***

### 263. Ugly Number

<img width="418" alt="{8FCC0A63-634D-47AA-90E5-E55FE46F1AC0}" src="https://github.com/user-attachments/assets/91729cdc-8123-4361-826a-2825946e9a75">

```
/**
 * @param {number} n
 * @return {boolean}
 */
var isUgly = function (num) {
    for (prime of [2, 3, 5]) {
        while (num && num % prime == 0) {
            num /= prime;
        }
    }
    return (num == 1);
};
```
Time and Space is O(1)
***



























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

### 62. Unique Paths

<img width="386" alt="image" src="https://github.com/user-attachments/assets/2b5ccd07-c525-4b00-8a54-eab97c622ae0">

```
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
Tine and Space O(M * N)
***

### 63. Unique Paths II

<img width="388" alt="image" src="https://github.com/user-attachments/assets/b9abeb76-4e23-45ac-9234-e73b1ce13a5a">

```
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function (obstacleGrid) {
    let m = obstacleGrid.length;
    if (m === 0) return 0;
    let n = obstacleGrid[0].length;
    if (n === 0) return 0;

    // If starting or ending cell has obstacle, no paths exist
    if (obstacleGrid[0][0] === 1 || obstacleGrid[m - 1][n - 1] === 1) {
        return 0;
    }

    // Initialize a 1D DP array
    let dp = new Array(n).fill(0);
    dp[0] = 1; // Start position

    // Initialize first row
    for (let j = 1; j < n; j++) {
        dp[j] = obstacleGrid[0][j] === 1 ? 0 : dp[j - 1];
    }

    // Iterate through each row starting from the second row
    for (let i = 1; i < m; i++) {
        // Update the first column for the current row
        dp[0] = obstacleGrid[i][0] === 1 ? 0 : dp[0];
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 1) {
                dp[j] = 0; // Obstacle cell
            } else {
                dp[j] = dp[j] + dp[j - 1];
            }
        }
    }

    return dp[n - 1];
};

```
***

### 120. Triangle

<img width="381" alt="image" src="https://github.com/user-attachments/assets/2ed18f17-1a8e-425d-bb16-c542b6daa6e7">

```
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    let n = triangle.length;

    // Start from the second-last row and work upwards
    for (let i = n - 2; i >= 0; i--) {
        for (let j = 0; j < triangle[i].length; j++) {
            // Update the current element with the sum of itself and the minimum of the two adjacent elements below
            triangle[i][j] += Math.min(triangle[i + 1][j], triangle[i + 1][j + 1]);
        }
    }

    // The top element contains the minimum path sum
    return triangle[0][0];
};

```
Time complexity
The time complexity of this solution is O(n^2), where n is the number of rows in the triangle. This is because we iterate through each element in the triangle once and perform constant time operations on each element.
Space complexity
The space complexity is O(1) because we are modifying the input triangle in place without using any additional data structures that grow with the input size.
***

### 931. Minimum Falling Path Sum

<img width="880" alt="image" src="https://github.com/user-attachments/assets/ae117970-a3d3-40e8-aef9-bd84e5e39db7">

```
/**
 * @param {number[][]} matrix
 * @return {number}
 */
var minFallingPathSum = function(matrix) {
    let m = matrix.length;
    
    for(let i = m - 2; i >= 0; i--) {
        for(let j = 0; j < m; j++) {
            let a = (j - 1 < 0) ? matrix[i + 1][j]: matrix[i + 1][j - 1];
            let b = (j + 1 > m - 1) ? matrix[i + 1][j]: matrix[i + 1][j + 1];
            let c = (j >= 0 && j <= m - 1) ? matrix[i + 1][j]: matrix[i + 1][j];
            matrix[i][j] += Math.min(a, b, c);
        }
    }
    return Math.min(...matrix[0]);
};
```
The time complexity of this solution is O(n^2) where n is the number of rows in the matrix. This is because we iterate through each cell in the matrix once and perform constant time operations on each cell.

The space complexity is O(1) because we are not using any extra space that scales with the input size. We are modifying the input matrix in place to store the minimum falling path sum.

***

### 416. Partition Equal Subset Sum

<img width="416" alt="image" src="https://github.com/user-attachments/assets/074955d6-d4be-4c80-b657-bd1fed9df5da">

```
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canPartition = function (nums) {
    let totalSum = 0;
    for (let i = 0; i < nums.length; i++) {
        totalSum += nums[i];
    }

    if (totalSum % 2 != 0) return false;

    let target = totalSum / 2;
    let dp = new Array(target + 1).fill(false);
    dp[0] = true;

    for (let num of nums) {
        for (let i = target; i >= num; i--) {
            if (dp[i - num]) dp[i] = true;
        }
    }

    return dp[target];
};
```
**Time complexity: O(N * Target)**
The time complexity of this solution is O(n * target), where n is the number of elements in the input array and target is the total sum divided by 2. This is because we iterate through each element in the input array and for each element, we iterate through the target sum.

**Space complexity: O(Target)**
The space complexity is O(target) because we are using a one-dimensional array of size target to store the intermediate results.

***

### 322. Coin Change

<img width="419" alt="image" src="https://github.com/user-attachments/assets/9d6eb299-c930-47dc-8278-055a9cfdda13">

```
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function(coins, amount) {
    let dp = new Array(amount + 1).fill(Infinity);
    dp[0] = 0;

    for(let coin of coins) {
        for(let i = coin; i <= amount; i++ ){
            dp[i] = Math.min(dp[i], dp[i - coin] + 1);
        }
    }

    return (dp[amount] == Infinity) ? -1 : dp[amount];
};
```
The time complexity of this solution is O(n * m), where n is the amount and m is the number of coins. This is because we iterate through each coin for each amount value.

The space complexity is O(n), where n is the amount. This is because we are using an array of size amount + 1 to store the minimum number of coins needed to make up each amount value.

***

### 494. Target Sum

<img width="418" alt="image" src="https://github.com/user-attachments/assets/f9f8eb2b-dc4f-4598-9d5e-164ea971a729">

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var findTargetSumWays = function (nums, target) {
    let totalSum = nums.reduce((acc, num) => acc + num, 0);

    if(totalSum < Math.abs(target) || (totalSum + target) % 2 !== 0) return 0;

    const subSetSum = (totalSum + target) / 2;

    const dp = new Array(subSetSum + 1).fill(0);
    dp[0] = 1;

    for(let num of nums) {
        for(let j = subSetSum; j >= num; j--) {
            dp[j] += dp[j - num];
        }
    }

    return dp[subSetSum];

};
```
The time complexity of this solution is O(n * target), where n is the number of elements in the input array nums and target is the target sum. This is because we iterate through each element in the nums array and for each element, we iterate through the subsetSum array, which has a size of target.

The space complexity is O(target) because we are using a DP array of size subsetSum to store the number of ways to reach each sum.

***

### 518. Coin Change II

<img width="418" alt="image" src="https://github.com/user-attachments/assets/bce7aa14-87c2-4664-80e1-1f4e9a502536">

```
/**
 * @param {number} amount
 * @param {number[]} coins
 * @return {number}
 */
var change = function(amount, coins) {
    let dp = new Array(amount + 1).fill(0);
    dp[0] = 1;

    for(let coin of coins) {
        for(let i = coin; i <= amount; i++) {
            dp[i] += dp[i - coin]; 
        } 
    }

    return dp[amount];
};
```
The time complexity of this solution is O(n*m), where n is the amount and m is the number of coins. This is because we iterate through each coin for each amount from 1 to the target amount.

The space complexity is O(n), where n is the amount. This is because we use an array of size amount + 1 to store the number of ways to make change for each amount.

***

### 1143. Longest Common Subsequence

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
Time O(M * N)
Space O(M * N)
***

### 516. Longest Palindromic Subsequence

<img width="418" alt="image" src="https://github.com/user-attachments/assets/3d3cd4da-1080-47c3-a824-5fe00a32e84f">

```
/**
 * @param {string} s
 * @return {number}
 */
var longestPalindromeSubseq = function (s) {
    let n = s.length;
    let dp = Array(n).fill().map(() => Array(n).fill(0));

    for (let i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;

        for (let j = i + 1; j < n; j++) {
            if (s[i] == s[j]) { // If the two characters match, the longest palindromic can be extended by two
                dp[i][j] = 2 + dp[i + 1][j - 1];
            } else {
                dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
            }
        }
    }

    return dp[0][n - 1];
};
```
Time andd Space is O(N * N)
***

### 45. Jump Game II

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function(nums) {
    let minJumps = 0;
    let [max, oldMax] = [0, 0]
    for(let i = 0; i < nums.length - 1; i++) {
        max = Math.max(max, i + nums[i]);

        if(i == oldMax) {
            minJumps++;
            oldMax = max;
        }
    }

    return minJumps;
};
```
Time: O(N) and Space O(1)

***

### 91. Decode Ways

<img width="415" alt="{13106358-EB1C-4A4F-95FF-140D4D894077}" src="https://github.com/user-attachments/assets/b6082cfe-d41c-4f04-879e-bc63af7a8e20">

<img width="413" alt="{67061FD2-80E9-4833-9DC3-59F868FB7BDA}" src="https://github.com/user-attachments/assets/e3574b38-623a-42c4-aa37-61f9593f7273">

```
/**
 * @param {string} s
 * @return {number}
 */
var numDecodings = function (s) {

    if (!s || s[0] === "0") return 0;

    let dp = new Array(s.length + 1).fill(0);
    dp[0] = 1;
    dp[1] = 1;

    for (let i = 2; i <= s.length; i++) {
        let oneDigit = parseInt(s[i - 1]);
        let twoDigits = parseInt(s.substring(i - 2, i));

        if (oneDigit !== 0) {
            dp[i] += dp[i - 1];
        }

        if (twoDigits >= 10 && twoDigits <= 26) {
            dp[i] += dp[i - 2];
        }
    }

    return dp[s.length];
};
```
Time and Space O(N)
***

### 96. Unique Binary Search Trees

<img width="415" alt="{57E43923-AD7F-4889-BD64-D868193FD7F4}" src="https://github.com/user-attachments/assets/047ef48b-6bdc-4e31-a8a6-b04e3127fe06">

```
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function(n) {
    let dp = new Array(n + 1).fill(0);
    dp[0] = 1; dp[1] = 1;

    for(let i = 2; i <= n; i++) {
        for(let j = 1; j <= i; j++) {
            dp[i] += dp[j - 1] * dp[i - j];
        }
    }

    return dp[n];
};
```
The time complexity of the given function `numTrees` is O(n^2). This is because there are two nested loops: the outer loop runs from 2 to n (which is n - 1 iterations), and the inner loop runs from 1 to i (which can be up to n iterations in the worst case). Therefore, the total number of operations is proportional to the sum of the first n integers, leading to a quadratic time complexity.

The space complexity is O(n). This is due to the use of the `dp` array, which stores the number of unique binary search trees that can be formed with a given number of nodes. The size of this array is n + 1, which simplifies to O(n) in terms of space complexity

***

### 95. Unique Binary Search Trees II

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number} n
 * @return {TreeNode[]}
 */
var generateTrees = function (n) {
    if (n == 0) return [];

    let constructTree = function (start, end) {
        if (start > end) return [null];

        let trees = [];

        for (let i = start; i <= end; i++) {
            let leftTree = constructTree(start, i - 1);
            let rightTree = constructTree(i + 1, end);

            for (let left of leftTree) {
                for (let right of rightTree) {
                    let tree = new TreeNode(i);
                    tree.left = left;
                    tree.right = right;
                    trees.push(tree);
                }
            }
        }
        return trees;
    };
    return constructTree(1, n);
}
```

***

### 97. Interleaving String

<img width="423" alt="{82E67946-4CBC-4C7E-9611-553A7F4A6E31}" src="https://github.com/user-attachments/assets/4ca03da1-95cc-44de-9cb6-098080fda0fb">


```
/**
 * @param {string} s1
 * @param {string} s2
 * @param {string} s3
 * @return {boolean}
 */
var isInterleave = function (s1, s2, s3) {
    if (s1.length + s2.length !== s3.length) return false;

    const dp = Array(s1.length + 1).fill(false).map(() => Array(s2.length + 1).fill(false));
    dp[0][0] = true;

    for (let i = 0; i <= s1.length; i++) {
        for (let j = 0; j <= s2.length; j++) {
            if (i > 0 && s1[i - 1] === s3[i + j - 1]) {
                dp[i][j] = dp[i][j] || dp[i - 1][j];
            }
            if (j > 0 && s2[j - 1] === s3[i + j - 1]) {
                dp[i][j] = dp[i][j] || dp[i][j - 1];
            }
        }
    }

    return dp[s1.length][s2.length];
};
```
Time and Space O(N * M)
***

### 122. Best Time to Buy and Sell Stock II

<img width="417" alt="{F180A2C9-9FBA-4B94-BE04-BDE3293D1BDD}" src="https://github.com/user-attachments/assets/b4f5ddbe-1278-46c5-b274-3ea7b4f49238">

```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
    let profitGained = 0;

    for (let i = 0; i < prices.length - 1; i++) {
        if (prices[i] < prices[i + 1]) {
            profitGained += (prices[i + 1] - prices[i]);
        }
    }

    return profitGained;
};

```
The time complexity of the given function `maxProfit` is O(n), where n is the length of the `prices` array. This is because the function iterates through the array once, performing a constant amount of work for each element (comparing and potentially adding to `profitGained`).

The space complexity is O(1), as the function uses a fixed amount of additional space regardless of the input size. It only utilizes a few variables (`profitGained` and the loop index `i`), which do not scale with the size of the input array. Thus, the function is efficient in both time and space.

***

### 139. Word Break

```
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function (s, wordDict) {
    let dp = new Array(s.length + 1).fill(false);
    dp[0] = true;

    for(let i = 0; i <= s.length; i++) {
        if(dp[i]) {
            for(let word of wordDict) {
                if(s.slice(i, i + word.length) == word) {
                    dp[i + word.length] = true; 
                }
            }
        }
    }

    return dp[s.length];
};
```
* Time complexity:
    The time complexity of the wordBreak function can be analyzed as follows:
    The outer loop runs from 0 to the length of the string s, which is O(n), where n is the length of s.
    Inside the outer loop, there is an inner loop that iterates over each word in the wordDict. If we denote the number of words in wordDict as m, then the inner loop runs O(m) times.
    For each word, the function checks if a substring of s matches the word, which takes O(k) time, where k is the length of the word. In the worst case, if we consider the average length of the words in the dictionary to be O(k), the total time spent in the inner loop can be approximated as O(m * k).
    Combining these factors, the overall time complexity is O(n * m * k).

* Space complexity:
    The space complexity of the function is primarily determined by the dp array, which has a size of n + 1. Thus, the space complexity is O(n).
***

### 221. Maximal Square

<img width="416" alt="{B157CD0D-ED67-4453-BBC1-A3A7C169FC11}" src="https://github.com/user-attachments/assets/02ed4b2a-0f51-4495-b2f3-c85e9640f086">

```
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalSquare = function (matrix) {
    if (matrix.length < 1) return 0;

    let rows = matrix.length;
    let cols = matrix[0].length;

    let dp = new Array(rows + 1).fill(0).map(() => new Array(cols + 1).fill(0));
    let max = 0;

    for (let row = 0; row < rows; row++) {
        for (let col = 0; col < cols; col++) {
            if (matrix[row][col] == '1') {
                dp[row + 1][col + 1] = Math.min(dp[row][col], dp[row + 1][col], dp[row][col + 1]) + 1;
                max = Math.max(max, dp[row + 1][col + 1]);
            }
        }
    }

    return max * max;
};
```
Time and Space is O(M * N)

***

### 264. Ugly Number II

![{71987ECD-C9FB-45F6-B275-13009C437F71}](https://github.com/user-attachments/assets/1d40025c-3474-49c2-8b0b-4f408257a1d7)

```

```

***





























## Hard

### 2035. Partition Array Into Two Arrays to Minimize Sum Difference

<img width="417" alt="image" src="https://github.com/user-attachments/assets/ce07e75a-36ac-4a2f-bf47-e74e49b3702d">

```
/**
 * @param {number[]} nums
 * @return {number}
 */
var minimumDifference = function(nums) {
    const n = nums.length / 2;
    const totalSum = nums.reduce((acc, num) => acc + num, 0);
    const target = totalSum / 2;
    
    // Split the array into two halves
    const left = nums.slice(0, n);
    const right = nums.slice(n);
    
    // Function to generate subset sums grouped by subset size
    const generateSubsetSums = (arr) => {
        const len = arr.length;
        const subsetSums = new Array(len + 1).fill(0).map(() => []);
        
        // Iterate over all possible subsets using bitmask
        for (let i = 0; i < (1 << len); i++) {
            let sum = 0;
            let size = 0;
            for (let j = 0; j < len; j++) {
                if (i & (1 << j)) {
                    sum += arr[j];
                    size++;
                }
            }
            subsetSums[size].push(sum);
        }
        
        // Sort the subset sums for each size for efficient binary searching
        for (let k = 0; k <= len; k++) {
            subsetSums[k].sort((a, b) => a - b);
        }
        
        return subsetSums;
    };
    
    const leftSums = generateSubsetSums(left);  // leftSums[k] = list of sums for subsets of size k
    const rightSums = generateSubsetSums(right); // rightSums[k] = list of sums for subsets of size k
    
    let minDiff = Infinity;
    
    // Iterate over possible subset sizes in the left half
    for (let k = 0; k <= n; k++) {
        const kLeft = k;
        const kRight = n - k;
        if (kRight < 0 || kRight > n) continue;
        
        const leftList = leftSums[kLeft];
        const rightList = rightSums[kRight];
        
        if (leftList.length === 0 || rightList.length === 0) continue;
        
        for (let sum1 of leftList) {
            // Find sum2 in rightList closest to (target - sum1)
            let needed = target - sum1;
            let idx = binarySearchClosest(rightList, needed);
            let sum2 = rightList[idx];
            let sumA = sum1 + sum2;
            let diff = Math.abs(2 * sumA - totalSum);
            if (diff < minDiff) minDiff = diff;
            
            // Also check the previous index if possible to find a closer sum
            if (idx > 0) {
                sum2 = rightList[idx - 1];
                sumA = sum1 + sum2;
                diff = Math.abs(2 * sumA - totalSum);
                if (diff < minDiff) minDiff = diff;
            }
        }
    }
    
    return minDiff;
};

/**
 * Helper function to find the index of the closest number to the target in a sorted array.
 * If two numbers are equally close, returns the smaller one.
 * @param {number[]} arr - Sorted array of numbers.
 * @param {number} target - The target number to find the closest to.
 * @return {number} - Index of the closest number.
 */
function binarySearchClosest(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    let bestIdx = -1;
    let minDiff = Infinity;
    
    while (left <= right) {
        let mid = Math.floor((left + right) / 2);
        let currentDiff = Math.abs(arr[mid] - target);
        
        if (currentDiff < minDiff) {
            minDiff = currentDiff;
            bestIdx = mid;
        }
        
        if (arr[mid] < target) {
            left = mid + 1;
        } else if (arr[mid] > target) {
            right = mid - 1;
        } else {
            // Exact match found
            return mid;
        }
    }
    
    return bestIdx;
}

```

***

### 44. Wildcard Matching

<img width="417" alt="image" src="https://github.com/user-attachments/assets/5e5f881e-d9a8-4738-8407-454a4f9664d8">

```
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function (s, p) {
    const m = s.length;
    const n = p.length;

    // Initialize DP table with false
    const dp = Array.from({ length: m + 1 }, () => Array(n + 1).fill(false));

    // Empty pattern matches empty string
    dp[0][0] = true;

    // Initialize first row (s is empty)
    for (let j = 1; j <= n; j++) {
        if (p[j - 1] === '*') {
            dp[0][j] = dp[0][j - 1];
        }
    }

    // Fill the DP table
    for (let i = 1; i <= m; i++) {
        for (let j = 1; j <= n; j++) {
            if (p[j - 1] === '*') {
                // '*' matches zero characters (dp[i][j - 1]) or one/more characters (dp[i - 1][j])
                dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
            } else if (p[j - 1] === '?' || p[j - 1] === s[i - 1]) {
                // Current characters match or pattern has '?'
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                // Characters do not match
                dp[i][j] = false;
            }
        }
    }

    return dp[m][n];
};
```
The time complexity of this solution is O(m*n), where m is the length of string s and n is the length of string p. This is because we are filling up a DP table of size (m+1) x (n+1) with nested loops iterating over m and n.

The space complexity of this solution is also O(m*n) because we are using a DP table of size (m+1) x (n+1) to store the intermediate results.

Overall, this solution uses dynamic programming to efficiently solve the problem of matching a string against a pattern, with a time and space complexity of O(m*n).

***

### 1312. Minimum Insertion Steps to Make a String Palindrome

<img width="414" alt="image" src="https://github.com/user-attachments/assets/45ead3a1-8f20-416c-884d-7f1e4a80e242">

```
/**
 * @param {string} s
 * @return {number}
 */
var minInsertions = function (s) {
    let n = s.length;
    let dp = new Array(n).fill(0);

    for (let i = n - 2; i >= 0; i--) {
        let prev = 0;

        for (let j = i + 1; j < n; j++) {
            const temp = dp[j];
            if (s[i] == s[j]) {
                dp[j] = prev;
            } else {
                dp[j] = Math.min(dp[j], dp[j - 1]) + 1;
            }

            prev = temp;
        }
    }

    return dp[n - 1];
};
```

Time O(N * N)
Space O(N)

***
