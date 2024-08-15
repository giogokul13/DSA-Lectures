# Problems

## Easy

### 13. Roman to Integer
Time O(N)
Space O(1)

```
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function (s) {
    let romanMap = {
        "I": 1, "V": 5, "X": 10, "L": 50, "C": 100,
        "D": 500, "M": 1000
    }
    let sum = 0;

    let i = s.length - 1;
    while (i >= 0) {
        if (romanMap[s[i]] > romanMap[s[i - 1]]) {
            sum += Math.abs(romanMap[s[i]] - romanMap[s[i - 1]])
            i -= 2;
        } else {
            sum += romanMap[s[i]];
            i -= 1;
        }
    }

    return sum;
};
```

***

### 14. Longest Common Prefix

The time complexity of this solution is O(n*m), where n is the number of strings in the input array and m is the length of the shortest string. This is because we iterate through each character of the shortest string and compare it with the corresponding characters in the other strings.

The space complexity is O(1) because we are using a constant amount of extra space, regardless of the size of the input.

```
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function (strs) {

    let prefix = strs[0];
    let prefixLen = prefix.length;

    for (let i = 1; i < strs.length; i++) {
        let str = strs[i];

        while (prefix !== str.substring(0, prefixLen)) {
            prefixLen--;
            if (prefixLen == 0) {
                return "";
            }
            prefix = prefix.substring(0, prefixLen);
        }
    }

    return prefix;
};
```

***





## Medium

### 151. Reverse Words in a String
Time is O(N)
Space is O(N)

```
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function (s) {
    let result = "";
    s = s.split(" ");
    for (let i = s.length - 1; i >= 0; i--) {
        if (s[i]) {
            result += s[i] + " ";
        }
    }

    return result.trim();
};
```

***

### 5. Longest Palindromic Substring

Time O(N * N)
Space O(1)

```
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
    let longestPalindromeStr = "";

    let findPalindromeString = (str, i, j) => {
        while( i >= 0 && j < str.length && str[i] == str[j]){
            i--;
            j++
        }

        return str.slice( i + 1, j);
    }

    for(let i = 0; i < s.length; i++){
        const str1 = findPalindromeString(s, i, i);
        const str2 = findPalindromeString(s, i, i + 1);

        let longerPalindrome = (str1.length > str2.length) ? str1 : str2;

        longestPalindromeStr = (longerPalindrome.length > longestPalindromeStr.length) ? longerPalindrome : longestPalindromeStr;
    }

    return longestPalindromeStr;
};
```

***

### 8. String to Integer (atoi)

Time O(N)
Space O(1)

```
/**
 * @param {string} s
 * @return {number}
 */

var myAtoi = function (s) {
    s = s.trim();  // Remove leading and trailing whitespace
    if (s.length === 0) {
        return 0;  // Handle empty string case
    }
    let num = 0;
    let i = 0;
    
    let sign = 1;  // 1 for positive, -1 for negative
    if (s[i] === '+') {
        i++;
    } else if (s[i] === '-') {
        sign = -1;
        i++;
    }

    while (i < s.length && /^\d$/.test(s[i])) {
        num = num * 10 + parseInt(s[i]);
        i++;
    }

    num *= sign;

    num = Math.max(Math.min(num, Math.pow(2, 31) - 1), -Math.pow(2, 31));  // Check for integer overflow
    
    return num;
}

```

***
