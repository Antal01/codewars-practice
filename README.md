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

