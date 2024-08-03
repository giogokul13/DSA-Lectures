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























## Hard

### 60. Permutation Sequence

```

```

***
