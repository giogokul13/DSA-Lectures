


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
