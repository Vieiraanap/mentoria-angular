# Chapter 3: JavaScript and TypeScript

## JavaScript
In order to write Angular code, we need to know about JavaScript. In this lesson, we focus on some features of modern JavaScript that are essential for Angular development.

Here are the topics you want to get up to speed with:

Variable scope: Differences between var, let, and const -> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let
Backticks and template strings -> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
Destructuring assignment syntax -> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
Arrow function syntax -> https://www.angulartraining.com/daily-newsletter/everything-you-need-to-know-about-arrow-functions/
Nullish coalescing operator -> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing

## TypeScript
TypeScript brings a lot of features to the table, and Angular relies on quite a few of these features such as decorators and class constructors.

In this lesson, we focus on the essentials of TypeScript for Angular development:

Definition of what is TypeScript -> https://www.typescriptlang.org/
Syntax for classes -> https://www.typescriptlang.org/docs/handbook/2/classes.html
Everyday types -> https://www.typescriptlang.org/docs/handbook/2/everyday-types.html
Union types and utility types -> https://blog.angulartraining.com/union-types-in-typescript-2517a82a1ea0 https://www.typescriptlang.org/docs/handbook/utility-types.html
Constructor syntax options -> https://www.typescriptlang.org/docs/handbook/2/classes.html#constructors
Enums -> https://www.typescriptlang.org/docs/handbook/enums.html#handbook-content

**QUIZ**

1. What's the value of `a` in this example?
let a = otherValue ?? 21

12 if otherValue == 12, 21 if otherValue is null


12 if otherValue === 12, 21 if otherValue is null or undefined [OK]


12 if otherValue === 12, 21 if otherValue is {} or undefined


"otherValue"

2. According to the following function signature:
function setCurrency(value: number, currency: 'USD' | 'GBP')
Which of the following code examples would compile:


setCurrency(10, 'USD'); [OK]

setCurrency('10', 'GBP');

setCurrency(10);

None of the above, the function syntax is incorrect

3. What does the following code output to the console?
enum UserResponse {
 No = 0,
 Yes = 1,
}

console.log(UserResponse.Yes);

1 [OK]


[object Object]

Yes


UserResponse.Yes

4. How many parameters does the following function expect?
function test(a, b, ...c) {
   // ...
}

exactly 3


None, this function signature is incorrect


2 to 5


at least 2 [OK]