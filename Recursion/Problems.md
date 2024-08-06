# Problems

## Easy


## Medium

### 39. Combination Sum
The time complexity of this combinationSum function is O(2^n) where n is the number of elements in the candidates array. This is because for each element in the candidates array, we have two recursive calls: one where we include the element in the combination and one where we exclude it. This results in a binary tree-like structure with 2 branches at each level, leading to a total of 2^n possible combinations.

The space complexity is O(n) where n is the number of elements in the candidates array. This is because the recursive calls and the temporary array 'temp' will have a maximum depth of n in the worst case scenario, as we are exploring all possible combinations.
```

var combinationSum = function (candidates, target) {
    var result = [];
    var temp = [];

    let search = (index, target) => {
        if(target == 0) return result.push(temp.slice());

        if(target < 0) return;

        if(index == candidates.length) return;

        temp.push(candidates[index]);

        search(index, target - candidates[index]);
        temp.pop();

        search(index + 1, target);
    }


    search(0, target);

    return result;
}
```

***


### 40. Combination Sum II

Time: O(2 ^ N)
Space:  O(N)

```
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
*/
var combinationSum2 = function (candidates, target) {
    var result = [];

    candidates.sort((a, b) => a - b);

    let search = (index, target, temp) => {
        if (target == 0) return result.push(temp.slice());

        if (target < 0) return;

        for (let i = index; i < candidates.length; i++) {

            if(i > index && candidates[i] == candidates[i - 1]) continue; // since the sorted array has the duplicates continue when there you encounter the previous element

            if(candidates[i] > target) break;

            search(i + 1, target - candidates[i], temp.concat(candidates[i]));
        }
    }

    search(0, target, []);

    return result;
};

```

*** 


### 131. Palindrome Partitioning

Time - O((2 ^ N) * N)
Space - O(N)

```
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function (s) {
    let result = [], part = [];

    let recurse = function (index) {

        if (index >= s.length) {
            result.push(part.slice());;
            return;
        }

        for (let i = index; i < s.length; i++) {
            if (isPalindrome(s, index, i)) {
                part.push(s.slice(index, i + 1));
                recurse(i + 1);
                part.pop();
            }
        }
    }

    recurse(0)

    return result;
};

let isPalindrome = function (string, left, right) {
    while (left < right) {
        if (string[left] != string[right]) return false;
        left++;
        right--;
    }

    return true;
}

```

[![YT Video](https://img.youtube.com/vi/3jvWodd7ht0/0.jpg)](https://www.youtube.com/watch?v=3jvWodd7ht0)


***

### 46. Permutations

The time complexity of this solution is O(n!) because there are n! possible permutations of the input array. The space complexity is also O(n!) because we are storing all possible permutations in the result array. This is because for each element in the input array, we recursively generate permutations of the remaining elements, resulting in n! recursive calls and permutations.

```
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function (nums) {

    if (nums.length == 1) return [nums.slice()];

    let result = [];

    for (let i = 0; i < nums.length; i++) {
        let n = nums.shift();
        var permutate = permute(nums.slice());

        for (let p of permutate) {
            p.push(n);
        }

        result.push(...permutate);
        nums.push(n);
    }

    return result;
};

```

[![YT Video](https://img.youtube.com/vi/s7AvT7cGdSo/0.jpg)](https://www.youtube.com/watch?v=s7AvT7cGdSo)

***




























## Hard

### 60. Permutation Sequence

```

```

***


### N Queens

The time complexity of this solution is O(N!), where N is the number of queens to be placed on the board. This is because there are N choices for the queen in the first row, N-2 choices for the queen in the second row (due to constraints from the first queen), N-4 choices for the queen in the third row, and so on. This results in a factorial time complexity.

The space complexity is O(N) for the sets used to keep track of the columns and diagonals, and O(N^2) for the board itself. Overall, the space complexity is O(N^2) due to the board.

```
/**
 * @param {number} n
 * @return {string[][]}
 */
var solveNQueens = function (n) {
    let col = new Set(), posDia = new Set(); // r + c 
    let negDia = new Set(); // ( r - c)

    let result = [];
    let board = Array(n).fill().map(() => Array(n).fill("."));

    let backtrack = (row) => {
        if (row == n) {
            result.push(board.map(r => r.join("")));
            return;
        }

        for (let c = 0; c < n; c++) {
            if (col.has(c) || posDia.has(row + c) || negDia.has(row - c)) continue;


            col.add(c);
            posDia.add(row + c);
            negDia.add(row - c);
            board[row][c] = "Q";

            backtrack(row + 1);

            col.delete(c);
            posDia.delete(row + c);
            negDia.delete(row - c);
            board[row][c] = ".";
        }
    }

    backtrack(0);

    return result;

};
```

[![YT Video](https://img.youtube.com/vi/Ph95IHmRp5M/0.jpg)](https://www.youtube.com/watch?v=Ph95IHmRp5M)

*** 


### 37. Sudoku Solver

Time: O(9^ (N * N))
Space: O(N * N);

```
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function (board) {
    solver(board, board.length);
};


var solver = (board, length) => {
    for (let row = 0; row < length; row++) {
        for (let col = 0; col < length; col++) {

            if (board[row][col] != ".") continue;

            for (let k = 1; k <= 9; k++) {
                let char = "" + k;
                if (isValid(board, row, col, length, char)) {
                    board[row][col] = char;

                    if (solver(board, length)) return true;
                }
            }

            board[row][col] = ".";
            return false;
        }
    }

    return true;
}


let isValid = (board, row, col, length, char) => {
    let entireRow = Math.floor(row / 3) * 3;
    let entireCol = Math.floor(col / 3) * 3;  //3, 2 ==> 3, 0 ==> 0, 2

    for (let i = 0; i < length; i++) {
        if (board[row][i] == char || board[i][col] == char) return false;
        let curRow = entireRow + Math.floor(i / 3);
        let curCol = entireCol + Math.floor(i % 3);

        if (board[curRow][curCol] == char) return false;
    }

    return true;
}

```

[![YT Video](https://img.youtube.com/vi/nC1rbW2YSz0/0.jpg)](https://www.youtube.com/watch?v=nC1rbW2YSz0)


***
