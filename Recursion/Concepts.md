

## Recursion

A function itself until a certain condition is met.

Stackoverflow - When thee is no limit / conditions set to terminate the function call in recursion - You end up in the state of Memory Stac Overflow.



Try

### Sum of n Numbers

n = 3

```
function sumOfN(n){
  let sum = 0;
  let recurse = function(n){
    if(n == 0 ) return;
    sum += n;
    recurse(n - 1);
  
  }

  return sum;
}

```

Another variation

```
function sumOfN(n){
  if(n < 1) return 0; 

  return n + sumOfN(n - 1);
}

```

Factorial of N

```
function Factorial(n){
  if(n < 1) return 1; 

  return n * sumOfN(n - 1);
}

```


 
***
