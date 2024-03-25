# codewars-practice  

## Playing with passphrases  
Everyone knows passphrases. One can choose passphrases from poems, songs, movies names and so on but frequently they can be guessed due to common cultural references. You can get your passphrases stronger by different means. One is the following:  

choose a text in capital letters including or not digits and non alphabetic characters,  

* shift each letter by a given number but the transformed letter must be a letter (circular shift),  
* replace each digit by its complement to 9,  
* keep such as non alphabetic and non digit characters,  
* downcase each letter in odd position, upcase each letter in even position (the first character is in position 0),  
* reverse the whole result.  
* Example:  
your text: "BORN IN 2015!", shift 1

1 + 2 + 3 -> "CPSO JO 7984!"

4 "CpSo jO 7984!"

5 "!4897 Oj oSpC"

With longer passphrases it's better to have a small and easy program. Would you write it?  

```
function playPass(s, n) {
    return s.split('').map((char, index) => {
    if (char.match(/[A-Za-z]/)) {
      let code = char.charCodeAt(0);
      if (code >= 65 && code <= 90) { // uppercase
        code = (code - 65 + n) % 26 + 65;
        char = String.fromCharCode(code);
        if (index % 2 === 0) char = char.toUpperCase();
        else char = char.toLowerCase();
      } else if (code >= 97 && code <= 122) { // lowercase
        code = (code - 97 + n) % 26 + 97;
        char = String.fromCharCode(code);
        if (index % 2 === 0) char = char.toUpperCase();
        else char = char.toLowerCase();
      }
    } else if (char.match(/[0-9]/)) {
      char = String(9 - parseInt(char));
    }
    return char;
  }).reverse().join('');
}
```
## Validate Credit Card Number  
In this Kata, you will implement the Luhn Algorithm, which is used to help validate credit card numbers.

Given a positive integer of up to 16 digits, return true if it is a valid credit card number, and false if it is not.

Here is the algorithm:

Double every other digit, scanning from right to left, starting from the second digit (from the right).

Another way to think about it is: if there are an even number of digits, double every other digit starting with the first; if there are an odd number of digits, double every other digit starting with the second:

1714 ==> [1*, 7, 1*, 4] ==> [2, 7, 2, 4]

12345 ==> [1, 2*, 3, 4*, 5] ==> [1, 4, 3, 8, 5]

891 ==> [8, 9*, 1] ==> [8, 18, 1]
If a resulting number is greater than 9, replace it with the sum of its own digits (which is the same as subtracting 9 from it):

[8, 18*, 1] ==> [8, (1+8), 1] ==> [8, 9, 1]  

or:

[8, 18*, 1] ==> [8, (18-9), 1] ==> [8, 9, 1]
Sum all of the final digits:

[8, 9, 1] ==> 8 + 9 + 1 = 18  

```
function validate(n){
  // Convert the number to a string and split it into an array of digits
  let digits = String(n).split('').map(Number);
  
  // Double every other digit starting from the second to last
  for (let i = digits.length - 2; i >= 0; i -= 2) {
    digits[i] *= 2;
    if (digits[i] > 9) {
      digits[i] -= 9;
    }
  }
  
  // Sum all the digits
  let sum = digits.reduce((acc, curr) => acc + curr, 0);
  
  // Check if the sum is divisible by 10
  return sum % 10 === 0;
}
```
## Fold an array  
In this kata you have to write a method that folds a given array of integers by the middle x-times.

An example says more than thousand words:

Fold 1-times:
[1,2,3,4,5] -> [6,6,3]

A little visualization (NOT for the algorithm but for the idea of folding):

 Step 1         Step 2        Step 3       Step 4       Step5
                     5/           5|         5\          
                    4/            4|          4\      
1 2 3 4 5      1 2 3/         1 2 3|       1 2 3\       6 6 3
----*----      ----*          ----*        ----*        ----*


Fold 2-times:
[1,2,3,4,5] -> [9,6]
As you see, if the count of numbers is odd, the middle number will stay. Otherwise the fold-point is between the middle-numbers, so all numbers would be added in a way.

The array will always contain numbers and will never be null. The parameter runs will always be a positive integer greater than 0 and says how many runs of folding your method has to do.

If an array with one element is folded, it stays as the same array.

The input array should not be modified!

Have fun coding it and please don't forget to vote and rank this kata! :-)

I have created other katas. Have a look if you like coding and challenges.

```
function foldArray(array, runs)
{
   let foldedArray = array.slice();
  
  for (let i = 0; i < runs; i++) {
    const halfLength = Math.floor(foldedArray.length / 2);
    const folded = [];
    
    for (let j = 0; j < halfLength; j++) {
      folded.push(foldedArray[j] + foldedArray[foldedArray.length - 1 - j]);
    }
    
    if (foldedArray.length % 2 !== 0) {
      folded.push(foldedArray[halfLength]);
    }
    
    foldedArray = folded;
  }
  
  return foldedArray;
}
```
## Reverse polish notation calculator  
Your job is to create a calculator which evaluates expressions in Reverse Polish notation.

For example expression 5 1 2 + 4 * + 3 - (which is equivalent to 5 + ((1 + 2) * 4) - 3 in normal notation) should evaluate to 14.

For your convenience, the input is formatted such that a space is provided between every token.

Empty expression should evaluate to 0.

Valid operations are +, -, *, /.

You may assume that there won't be exceptional situations (like stack underflow or division by zero).

```
function calc(expr) {
 if (expr === "") return 0;
  
  const tokens = expr.split(" ");
  const stack = [];
  
  for (const token of tokens) {
    if (!isNaN(token)) {
      stack.push(parseFloat(token));
    } else {
      const b = stack.pop();
      const a = stack.pop();
      switch (token) {
        case "+":
          stack.push(a + b);
          break;
        case "-":
          stack.push(a - b);
          break;
        case "*":
          stack.push(a * b);
          break;
        case "/":
          stack.push(a / b);
          break;
      }
    }
  }
  
  return stack.pop();
}
```
## Kebabize  
Modify the kebabize function so that it converts a camel case string into a kebab case.

"camelsHaveThreeHumps"  -->  "camels-have-three-humps"
"camelsHave3Humps"  -->  "camels-have-humps"
"CAMEL"  -->  "c-a-m-e-l"
Notes:

the returned string should only contain lowercase letters  
```
function kebabize(str) {
  return str
    .replace(/[0-9]/g, '') 
    .replace(/([A-Z])/g, '-$1') 
    .toLowerCase() 
    .replace(/^-/, ''); 
}
```
## Word a10n (abbreviation)  
The word i18n is a common abbreviation of internationalization in the developer community, used instead of typing the whole word and trying to spell it correctly. Similarly, a11y is an abbreviation of accessibility.

Write a function that takes a string and turns any and all "words" (see below) within that string of length 4 or greater into an abbreviation, following these rules:

A "word" is a sequence of alphabetical characters. By this definition, any other character like a space or hyphen (eg. "elephant-ride") will split up a series of letters into two words (eg. "elephant" and "ride").
The abbreviated version of the word should have the first letter, then the number of removed characters, then the last letter (eg. "elephant ride" => "e6t r2e").
Example
abbreviate("elephant-rides are really fun!")
//          ^^^^^^^^*^^^^^*^^^*^^^^^^*^^^*
// words (^):   "elephant" "rides" "are" "really" "fun"
//                123456     123     1     1234     1
// ignore short words:               X              X

// abbreviate:    "e6t"     "r3s"  "are"  "r4y"   "fun"
// all non-word characters (*) remain in place
//                     "-"      " "    " "     " "     "!"
=== "e6t-r3s are r4y fun!"  

```
function abbreviate(string) {
   return string.replace(/[a-zA-Z]{4,}/g, match => {
    return match[0] + (match.length - 2) + match[match.length - 1];
  });
}
```
## Matrix Addition    
Write a function that accepts two square matrices (N x N two dimensional arrays), and return the sum of the two. Both matrices being passed into the function will be of size N x N (square), containing only integers.

How to sum two matrices:

Take each cell [n][m] from the first matrix, and add it with the same [n][m] cell from the second matrix. This will be cell [n][m] of the solution matrix. (Except for C where solution matrix will be a 1d pseudo-multidimensional array).

Visualization:

|1 2 3|     |2 2 1|     |1+2 2+2 3+1|     |3 4 4|
|3 2 1|  +  |3 2 3|  =  |3+3 2+2 1+3|  =  |6 4 4|
|1 1 1|     |1 1 3|     |1+1 1+1 1+3|     |2 2 4|    

```
function matrixAddition(a, b){
 const n = a.length; 
  const result = []; 
  
  for (let i = 0; i < n; i++) {
    result.push([]); 
    for (let j = 0; j < n; j++) {
      result[i][j] = a[i][j] + b[i][j];
    }
  }
  
  return result;
}
```
## Length of missing array    
You get an array of arrays.
If you sort the arrays by their length, you will see, that their length-values are consecutive.
But one array is missing!


You have to write a method, that return the length of the missing array.

Example:
[[1, 2], [4, 5, 1, 1], [1], [5, 6, 7, 8, 9]] --> 3

If the array of arrays is null/nil or empty, the method should return 0.

When an array in the array is null or empty, the method should return 0 too!
There will always be a missing element and its length will be always between the given arrays.

Have fun coding it and please don't forget to vote and rank this kata! :-)

I have created other katas. Have a look if you like coding and challenges.    
```
function getLengthOfMissingArray(arrayOfArrays) {
 if (!arrayOfArrays || arrayOfArrays.some(arr => !arr || arr.length === 0)) {
        return 0; // Handle null, empty array, or array with empty sub-arrays
    }

    arrayOfArrays.sort((a, b) => a.length - b.length); // Sort arrays by length

    for (let i = 0; i < arrayOfArrays.length - 1; i++) {
        if (arrayOfArrays[i + 1].length !== arrayOfArrays[i].length + 1) {
            return arrayOfArrays[i].length + 1; // Return the missing length
        }
    }

    return 0; // Return 0 if no missing length is found
}
```
## Maze Runner    
Introduction
Welcome Adventurer. Your aim is to navigate the maze and reach the finish point without touching any walls. Doing so will kill you instantly!
Task
You will be given a 2D array of the maze and an array of directions. Your task is to follow the directions given. If you reach the end point before all your moves have gone, you should return Finish. If you hit any walls or go outside the maze border, you should return Dead. If you find yourself still in the maze after using all the moves, you should return Lost.
The Maze array will look like

maze = [[1,1,1,1,1,1,1],
        [1,0,0,0,0,0,3],
        [1,0,1,0,1,0,1],
        [0,0,1,0,0,0,1],
        [1,0,1,0,1,0,1],
        [1,0,0,0,0,0,1],
        [1,2,1,0,1,0,1]]
..with the following key

      0 = Safe place to walk
      1 = Wall
      2 = Start Point
      3 = Finish Point
  direction = ["N","N","N","N","N","E","E","E","E","E"] == "Finish"
Rules
1. The Maze array will always be square i.e. N x N but its size and content will alter from test to test.

2. The start and finish positions will change for the final tests.

3. The directions array will always be in upper case and will be in the format of N = North, E = East, W = West and S = South.

4. If you reach the end point before all your moves have gone, you should return Finish.

5. If you hit any walls or go outside the maze border, you should return Dead.

6. If you find yourself still in the maze after using all the moves, you should return Lost.    ű
   
```
   function mazeRunner(maze, directions) {
    let startPos = { x: -1, y: -1 };
    for (let i = 0; i < maze.length; i++) {
        for (let j = 0; j < maze[i].length; j++) {
            if (maze[i][j] === 2) {
                startPos = { x: i, y: j };
                break;
            }
        }
    }
    
    const directionsMap = {
        N: { x: -1, y: 0 },
        S: { x: 1, y: 0 },
        E: { x: 0, y: 1 },
        W: { x: 0, y: -1 }
    };

    let currentPos = { ...startPos };

    for (const dir of directions) {
        const move = directionsMap[dir];
        currentPos.x += move.x;
        currentPos.y += move.y;

        if (
            currentPos.x < 0 || currentPos.x >= maze.length ||
            currentPos.y < 0 || currentPos.y >= maze[0].length
        ) {
            return "Dead"; 
        }

        const cell = maze[currentPos.x][currentPos.y];

        if (cell === 1) {
            return "Dead";
        } else if (cell === 3) {
            return "Finish";
        }
    }

    return "Lost"; 
    }
```
## New Cashier Does Not Know About Space or Shift    
Some new cashiers started to work at your restaurant.

They are good at taking orders, but they don't know how to capitalize words, or use a space bar!

All the orders they create look something like this:

"milkshakepizzachickenfriescokeburgerpizzasandwichmilkshakepizza"

The kitchen staff are threatening to quit, because of how difficult it is to read the orders.

Their preference is to get the orders as a nice clean string with spaces and capitals like so:

"Burger Fries Chicken Pizza Pizza Pizza Sandwich Milkshake Milkshake Coke"

The kitchen staff expect the items to be in the same order as they appear in the menu.

The menu items are fairly simple, there is no overlap in the names of the items:

1. Burger
2. Fries
3. Chicken
4. Pizza
5. Sandwich
6. Onionrings
7. Milkshake
8. Coke
```
function getOrder(input) {
  const menuItems = [
    "Burger", "Fries", "Chicken", "Pizza", 
    "Sandwich", "Onionrings", "Milkshake", "Coke"
  ];
  let formattedOrder = [];

  menuItems.forEach(item => {
    const regex = new RegExp(item.toLowerCase(), 'g');
    const count = (input.match(regex) || []).length;

    for (let i = 0; i < count; i++) {
      formattedOrder.push(item);
    }
  });

  // Convert the array to a string with proper formatting
  return formattedOrder.join(" ");
}
```
## ROT13
How can you tell an extrovert from an introvert at NSA?
Va gur ryringbef, gur rkgebireg ybbxf ng gur BGURE thl'f fubrf.

I found this joke on USENET, but the punchline is scrambled. Maybe you can decipher it?
According to Wikipedia, ROT13 is frequently used to obfuscate jokes on USENET.

For this task you're only supposed to substitute characters. Not spaces, punctuation, numbers, etc.

Test examples:

"EBG13 rknzcyr." -> "ROT13 example."

"This is my first ROT13 excercise!" -> "Guvf vf zl svefg EBG13 rkprepvfr!"    
```
function rot13(str) {
  let result = '';

  for (let i = 0; i < str.length; i++) {
    let charCode = str.charCodeAt(i);

    if (charCode >= 97 && charCode <= 122) {
      charCode = ((charCode - 97 + 13) % 26) + 97;
    }
    else if (charCode >= 65 && charCode <= 90) {
      charCode = ((charCode - 65 + 13) % 26) + 65;
    }

    result += String.fromCharCode(charCode);
  }

  return result;
}
```
## Memoized Fibonacci    
The Fibonacci sequence is traditionally used to explain tree recursion.

function fibonacci(n) {
    if(n==0 || n == 1)
        return n;
    return fibonacci(n-1) + fibonacci(n-2);
}
This algorithm serves welll its educative purpose but it's tremendously inefficient, not only because of recursion, but because we invoke the fibonacci function twice, and the right branch of recursion (i.e. fibonacci(n-2)) recalculates all the Fibonacci numbers already calculated by the left branch (i.e. fibonacci(n-1)).

This algorithm is so inefficient that the time to calculate any Fibonacci number over 50 is simply too much. You may go for a cup of coffee or go take a nap while you wait for the answer. But if you try it here in Code Wars you will most likely get a code timeout before any answers.

For this particular Kata we want to implement the memoization solution. This will be cool because it will let us keep using the tree recursion algorithm while still keeping it sufficiently optimized to get an answer very rapidly.

The trick of the memoized version is that we will keep a cache data structure (most likely an associative array) where we will store the Fibonacci numbers as we calculate them. When a Fibonacci number is calculated, we first look it up in the cache, if it's not there, we calculate it and put it in the cache, otherwise we returned the cached number.

Refactor the function into a recursive Fibonacci function that using a memoized data structure avoids the deficiencies of tree recursion. Can you make it so the memoization cache is private to this function?

```
function fibonacci(n) {
  const cache = {};

  function fibMemoized(n) {
    if (cache[n]) {
      return cache[n];
    }

    if (n < 2) {
      return n;
    }

    cache[n] = fibMemoized(n - 1) + fibMemoized(n - 2);

    return cache[n];
  }

  return fibMemoized(n);
}
```
## Convert A Hex String To RGB    
When working with color values it can sometimes be useful to extract the individual red, green, and blue (RGB) component values for a color. Implement a function that meets these requirements:

Accepts a case-insensitive hexadecimal color string as its parameter (ex. "#FF9933" or "#ff9933")
Returns a Map<String, int> with the structure {r: 255, g: 153, b: 51} where r, g, and b range from 0 through 255
Note: your implementation does not need to support the shorthand form of hexadecimal notation (ie "#FFF")

Example
"#FF9933" --> {r: 255, g: 153, b: 51}    
```
function hexStringToRGB(hexString) {
  hexString = hexString.replace('#', '');

  const rHex = hexString.substring(0, 2);
  const gHex = hexString.substring(2, 4);
  const bHex = hexString.substring(4, 6);

  const r = parseInt(rHex, 16);
  const g = parseInt(gHex, 16);
  const b = parseInt(bHex, 16);

  return { r, g, b };
}
```

