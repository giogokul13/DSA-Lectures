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

### 28. Find the Index of the First Occurrence in a String

Time O(N) and Space O(1)

```
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
    return haystack.indexOf(needle);
};

```
*** 

### 242. Valid Anagram

Time and Space  is O(N)

```
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */

var isAnagram = function (s, t) {
    if (s.length !== t.length) return false;  // Early return if lengths are not equal

    let map = new Map();

    // Count frequency of each character in string s
    for (let char of s) {
        map.set(char, (map.get(char) || 0) + 1);
    }

    // Decrease frequency for each character in string t
    for (let char of t) {
        if (!map.has(char)) return false;  // Character not found in map

        map.set(char, map.get(char) - 1);
        
        if (map.get(char) === 0) map.delete(char);  // Remove char from map if count goes to 0
    }

    // If map is empty, the strings are anagrams
    return map.size === 0;
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


### 686. Repeated String Match

Time O(M + N)
Space O(1)

```
/**
 * @param {string} a
 * @param {string} b
 * @return {number}
 */
var repeatedStringMatch = function (a, b) {
    let init = a;
    let count = 1;

    while (a.length < b.length) {
        a += init;
        count++;
    }

    count = (a.indexOf(b) > -1) ? count : ((a + init).indexOf(b) > -1) ? count + 1 : -1;

    return count;
};

```

***


### 38. Count and Say

The **time complexity** of this solution is O(2^n) because for each iteration, the length of the result string doubles. 

The **space complexity** is O(2^n) as well because we are storing the result string for each iteration.

```
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function (n) {

    let result = "1";

    if (n == 1) return "1"

    let count = 0;

    for (let i = 1; i < n; i++) {
        count = 1;
        let temp = "";
        let j = 0;

        while (j < result.length) {
            if (result[j] === result[j + 1]) {
                count++;
            } else {
                temp += count + result[j];
                count = 1;
            }
            j++;
        }
        result = temp;
    }

    return result;
};
```

***


### 165. Compare Version Numbers

Time O(N) Space O(1)

- Solution 1
```
/**
 * @param {string} version1
 * @param {string} version2
 * @return {number}
 */
var compareVersion = function (version1, version2) {

    let i = 0, j = 0;
    let v1 = 0, v2 = 0;
    let result = 0;

    while (i < version1.length && j < version2.length) {

        while (i < version1.length && version1[i] != ".") {
            v1 *= 10 + pareInt(version1[i]);
            i++;
        }

        while (j < version2.length && version2[j] != ".") {
            v2 *= 10 + pareInt(version2[i]);
            j++;
        }

        if (v1 > v2) result = 1;
        if (v1 < v2) result = -1;

    }
    return 0;

};

```
- Solution 2
Time O(N) Space O(N)

```
/**
 * @param {string} version1
 * @param {string} version2
 * @return {number}
 */
var compareVersion = function (version1, version2) {
    let v1 = version1.split('.');
    let v2 = version2.split('.');
    let len = Math.max(v1.length, v2.length);

    for (let i = 0; i < len; i++) {
        let num1 = i < v1.length ? parseInt(v1[i], 10) : 0;
        let num2 = i < v2.length ? parseInt(v2[i], 10) : 0;

        if (num1 < num2) return -1;
        if (num1 > num2) return 1;
    }

    return 0;
};

```


***
