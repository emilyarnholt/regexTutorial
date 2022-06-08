# Email Validation - Regex tutorial 

This tutorial surrounds the use of regex when matching emails. We are going to be looking at the expression: 
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
This is used when you need to validate emails in technology like Node Inqurier or when you need to test if an email is valid on a website. 

## Summary

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

This expression is used to validate email addresses. This tutorial walks through the components of a regex and how it applies to this sequence.  

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
In the example ^ is the first anchor. This allows the computer to know at the beginning of the string there must be a match. For example, your email address can't be #emilynarnholt@gmail.com this is not valid, because this string is not a correct email due to the # in the beginning. This does not match the terms in your regex. To make it valid you would need to remove the # in the front of the string. 

Example: 

const str1 = 'emilynarnholt@gmail.com'

const str2 = '#emilynarnholt@gmail.com'

// with the ^ anchor 
const regex = new RegExp(/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/);

console.log(regex.test(str1));
// expected output: true

console.log(regex.test(str2));
// expected output: false 

If you didn't have the ^ anchor, both of the tests would return as true 

const str1 = 'emilynarnholt@gmail.com'

const str2 = '#emilynarnholt@gmail.com'

// with the ^ anchor 
const regex = new RegExp(/([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/);

console.log(regex2.test(str1));
// expected output: true

console.log(regex2.test(str2));
// expected output: true


The second anchor, $, is found at the end of the regular expression. The $ shows that the you are matching the strong that ends with the terms that are coming before it. Meaning, if the end of the string is not valid then due to the regex definied, the string is not a match. It is disqualified. 

Heres an example:

const str1 = 'emilynarnholt@gmail.com';

const str2 = 'emilynarnholt@gmail.com#';

// with $ anchor
const regex = new RegExp(/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/);

console.log(regex.test(str1));
// expected output: true 

console.log(regex.test(str2));
// expected output: false 

// without $ anchor
const regex2 = new RegExp(/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})/);

console.log(regex2.test(str1));
// expected output: true 

console.log(regex2.test(str2));
// expected output: true 

### Quantifiers

Quanitfies are used to limit the string, also the section of the string that the regex matches. At the end of the regex look at the expression: .([a-z\.]{2,6}). {2,6} is the quantifier. This says hat the specific part of the string has to be between 2 and 6 characters long. This lets the string end in ".com", ".net" ".co" these are all valid emails and strings, but emails that end in ".thisismyemail" etc. are not valid.

In our regex use used a + in the end of the two subexpressions. This shows that the regex matches a pattern one or more times. Anything before the @ needs to be 1 or more characters to create a match. It is the same with the middle subexpression. 
### OR Operator
You would use an OR Operator to match multiple patterns, the OR Operator is | you use this in strings. This or that patterns are very common. 
For example: 
hello|hi 
This is a string containing either hello or hi.
(a|bc)de 
This is a string containing either ade or bcde. 
### Character Classes
Character classes are defined as a set of characters that will end in a match. \d is an example found in our regex, this is a set of all numbers and bracket expressions, this is similar to custom character classes. Same with . Any unescape dot matches any character except the newline character. 
### Flags
Flags are something that effect the search, there are 6 in JavaScript. 
i : this makes the search case-insensitive, meaning theres no difference between A and a. 
g : this makes the search look for all of the matches, not just the first match is returned. 
m : this means multiline mode. This affects ^ and $ they match the beginning and the end of the string but the start and end of the line 
s : this allows "dotall" mode, which is a . to match a newline character /n 
u : this allows Unicode support fully, this allows the correct processing of surrogate pairs. 
y: this is sticky mode, the exact position in the text 

### Grouping and Capturing
You use grouping constructs to make different sections. This is also known as a subexpression found in our regex: ([a-z0-9_\.-]+), ([\da-z\.-]+), and ([a-z\.]{2,6}). To make a subexpresion, you put it in parentheses.

### Bracket Expressions

Bracket expressions are the bulk of our regex. They are also called positive character groups. What they do is define the characters as valid when matching a string. [a-z0-9_\.-] is our first bracket expression. Looking t the first term a-z is a defining range if characters, "a" through "z". This is for the entire alphabet being valid. If you wanted to have 'a' through 'd' is valid you would use a-d. This includes the letters "a" "b" "c" and "d". To define a range you use "-". Another option is to define a specific set. For example you could want to use "a" "b" and "d" in the set. To do so you would write abd in your square brackets. This shows that "a" "b" and "d" are all valid. To include upper and lowcase characters in your range you would write [a-zA-z] if you wanted to use the entire alphabet. 

In order to include numbers, and include all numbers you would use 0-9. This includes 0,1,2,3,4,5,6,7,8, and 9. You would add this to your bracket expression. [a-z0-9]. 

Next in the positive character group is a list of special characters. You will use _\.-, this says you can use an underscore _, a hyphen - and a dot \. The backslash is called escaping a character. 

The next positive character group is [\da-z\.-]. \d means "arabic numeral digit" is a match. Before it was written as 0-9, now it is \d. 
### Greedy and Lazy Match
Greedy is when your expression matches the largest group possible and lazy match means it matches the smallest group possible.
For Greedy it keeps searching until the condition is unsatisfied. For Lazy it stops searching once the condition is satisfied. 
The + Quantifier is a Greedy match, will match as many times as it can. The {} us another Greedy match, whn it finds the match '{2,6} is the very last capture group.  
### Boundaries
/b is a boundary. This matches positions where one side is a character, letter, digit, underscore etc, the other side is not a word character. It can be a space character or thr beginning of the string. 
### Back-references
The () used matches the opening and closing HTML tags with the text in between see the examples below. 
([a-z0-9_\.-]+) 
([\da-z\.-]+) 
([a-z\.]{2,6})
### Look-ahead and Look-behind
These are used when you need to find matches to a pattern that are followed or preceeded by another pattern. When used together it is commonly known as "lookaround". 
## Author

Emily Arnholt is a junior full stack developer based in Nashville, Tennessee. She attends Vanderbilt University's Full Stack Web Development program. Her Github is linked below
https://github.com/emilyarnholt