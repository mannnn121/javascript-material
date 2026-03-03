## Variables
The first element of programming that we will talk about is the **variable**. You may know the name of a variable from mathematics, where it means a symbol used as a placeholder for different values that can change. They have a similar role in programming.

What do we actually need them for? As you can guess, most programs are quite complex, and we are rarely able to solve the problem with a single operation. Usually, the program will consist of many more operations, each of which can produce some intermediate results, which will be needed in the next steps. Variables allow us to store such results, to modify them, or to feed them into subsequent operations.

## Naming the variables
In most programming languages, a variable must be declared before use, and JavaScript is no exception. Declaring a variable is simply "reserving" the name of the variable. This way, we inform the program that in the further part of the execution, we will use this name to refer to our container, in order to retrieve a value from it, or save a value to it.

In JavaScript, variable names may consist of any sequence of letters (lower-case and upper-case), digits, underscore characters, and dollar signs, but they must not start with a digit. There is a list of reserved words that cannot be used as variable names (look at the table below).

The important thing is also that the JavaScript interpreter distinguishes between lower-case and upper-case letters, also in variable names, so names such as test, Test, or TEST will be treated as different.

The names of of variables in JavaScript can be virtually any character string. However, there is a set of reserved word that cannot be used  to name variables, functions, or anything else. They are integral parts of the language and are assigned meaning that cannot be changed. Below you will find a list of them.
- abstract
- break
- char
- debugger

| **abstract** | **arguments** | **await**  | **boolean**  |
| ------------ | ------------- | ---------- | ------------ |
| **break**    | **byte**      | **case**   | **switch**   |
| **char**     | **class**     | **const**  | **continue** |
| **debugger** | **default**   | **delete** | **do**       |

## Declaring Variables
As we mentioned before, we **declare** the variable to reserve a name for it. This is a simplification, because in fact, memory space is also reserved for the variable, but when programming in JavaScript, we practically never have to think about what happens in the memory. Usually, the values stored in the variable will be able to be modified during the execution of the program (they are "variables", after all). Why usually? Because we can declare variables whose values cannot be changed. To be honest, we don't even call them variables anymore – we call them **constants**. For the declarations, we use the keywords `var` or `let` for **variables** and `const` for **constants**. For now, however, let's stay with the usual variables, and we will return to the constants in a moment.

```
var height;
console.log(height); // -> undefined
console.log(width); // -> Uncaught ReferenceError: weight is not defined
```

The first line is the variable **declaration** (we can see the `var` keyword). This declaration means that the word height will be treated as the name of the container for certain values.

The declaration, like other JavaScript instructions, should end with a semicolon. In the second line, we try to write out the value of this variable (that is, what is in the container) on the console. Because we haven't put anything there yet, the result is undefined (the interpreter knows this variable, but it has no value yet – the value is undefined). In the next line, we try to print out the contents of the weight variable ... which we forgot to declare. This time, we will see `ReferenceError`. The JavaScript interpreter, which executes our program, has informed us that it doesn’t know a variable by this name (so the variable itself is undefined).

The alternative to it is the keyword `let`. We use both keywords in the same way. Both are meant for declaring variables, and both can be found in different examples on the Internet or in books. However, they are not exactly the same, and we’ll discuss the differences in their operation later in this chapter (even in several places).

The keyword `var` comes from the original JavaScript syntax, and the keyword `let` was introduced much later. Therefore, you will find `var` more in older programs. Currently, it is highly recommended to use the word `let` for reasons that we’ll discuss in a moment.

So, let's take a look at our example rewritten this time using the keyword `let`.

```
let height;
console.log(height); // -> undefined
```

One of the basic differences in the use of _var_ and _let_ is that let prevents us from declaring another variable with the same name (an error is generated). Using _var_ allows you to re-declare a variable, which can potentially lead to errors in the program execution.

```
var height;
var height;
console.log(height); // -> undefined
```

The example above demonstrates the possibility of re-declaring a variable using the keyword var. In this situation, it will not cause an error, but in more complex programs a redeclaration, especially by accident, may no longer be without consequences. When declaring with let, the interpreter checks whether such a variable has already been declared, no matter if let or var is used in the previous declaration.

```
let height;
let height; // -> Uncaught SyntaxError: Identifier 'height' has already been declared
console.log(height);
```

So use `let` to declare variables, if only because you don't want to accidentally declare a variable again.

## Initializing Variables
After a successful declaration, the variable should be **initialized**, in other words, it should be given its first value. **Initialization** is done by assigning a certain value to a variable (indicated by its name). To assign it, we use the operator `=`.

You can assign to a variable: a specific value; the contents of another variable; or, for example, the result returned by a function.

Initialization can be done either together with the declaration, or separately as an independent command. It is important to enter the first value into the variable before trying to read, modify, or display it.

```
let height = 180;
let anotherHeight = height;
let weight;
console.log(height); // -> 180
console.log(anotherHeight); // -> 180
weight = 70;
console.log(weight); // -> 70
```

In the above example (check it in the editor), the declarations of the variables height and anotherHeight are combined with their initialization, while the variable weight is declared and initialized separately. The height and weight variables are initialized by providing specific values (more precisely, a number), while the anotherHeight variable receives a value read from the height variable. The values of all the variables are displayed on the console.

By the way, pay attention to one thing. If you specify a variable name in console.log, the interpreter recognizes it and displays its value. If you put the same name in quotation marks, it will be treated as plain text, and displayed as such.

```
let height = 180;
console.log(height) // -> 180
console.log("height") // -> height
```

## Declarations and strict mode
JavaScript had some major changes introduced in 2009 and 2015. Most of these changes extended the language syntax with new elements, but some of them concerned only the operation of the JavaScript interpreters. Often it was about clarifying the interpreters' behavior in potentially erroneous situations, such as in cases of variable initialization without any prior declaration.

Let's look at an example:
```
height = 180;
console.log(height); // -> 180
```

At first glance, you can see that we’ve forgotten to declare the variable height. The original JavaScript syntax allowed for such negligence, and at the moment of initialization it made this declaration for us. It seems like quite a good solution, but unfortunately it can sometimes lead to ambiguous and potentially erroneous situations (we’ll say a few more words about it while discussing the scope).

Let's modify our example:
```
"use strict";

height = 180; // -> Uncaught ReferenceError: height is not defined
console.log(height);
```

At the beginning of our code, we’ve added `"use strict";`. This statement has radically changed the behavior of the interpreter. Why? We use it when we want to force the interpreter to behave according to modern JavaScript standards. So, as long as you aren’t running some really old code, you should always use it. And this time, using a variable without its previous declaration is treated as an error.

The sentence `"use strict";` must be placed at the very beginning of the code. It will cause the interpreter to deal with the rest of the code using strict mode, which is the modern JavaScript standard. All further examples in our course will be prepared to work in this mode by default, even if `"use strict";` does not always appear at the beginning of the code.

## Changing variables values
Variables, as their name suggests, can store data that will vary. Changes are made by assigning a new value to the variable, which overwrites the previous one.

```
let steps = 100;
console.log(steps); // -> 100
steps = 120
console.log(steps); // -> 120
steps = steps + 200;
console.log(steps); // -> 320
```

In our example, we’ve declared a variable called steps. Initially, it contains the number 100, which is then changed to 120. Then we add 200 to the current contents of the variable, as a result of which the variable contains 320.

Variables in the JavaScript language are untyped (or, to be more precise, they are weakly and dynamically typed). This means that JavaScript will not control what type of value we store in the variable. What exactly is the data type? You can probably intuitively answer this question yourself. The type determines the belonging of a given data to a certain set that share the same properties and on which you can perform the same operations. Data types vary greatly depending on the programming language. In JavaScript, the main types are number and character string. We will talk much more about types in the next chapter. Let's declare a few variables and initialize them with values of different types:

```
let greeting = "Hello";
let counter = 100
```

As you can see, the greeting variable is initiated with a value of the string type, while the counter variable is initiated with a value of the number type. Continuing the example, we will make a small change in the contents of the greeting variable.

```
console.log(greeting); // -> Hello
greeting = 1;
console.log(greeting); // -> 1
```

JavaScript allows us to easily replace the greeting variable with a value whose type is different from the one originally stored there. JavaScript goes one step further and not only allows us to change the types of values kept in a variable, but it also performs their implicit conversion if necessary (we will also return to this topic of conversion when discussing types). Let's restore the original value of the greeting variable and then add the value of the counter variable to it.

```
greeting = "Hello!";
greeting = greeting + counter;
console.log(greeting) // -> Hello!100
```

The interpreter will check the type of value stored in the greeting variable and convert the value from the counter variable to the same type before performing an addition operation. As a result, the string `"100"` will be added to the `"Hello!"` character string and stored to the greeting variable. By the way, note that JavaScript interprets `100` as a number, but `"100"` as a string.

## Constants
The `const` keyword is used to declare containers similar to variables. Such containers are called **constants**. Constants are also used to store certain values, but once values have been entered into them during initialization, they can no longer be modified. This means that this type of container is simultaneously declared and initialized. For example, the following declaration of the greeting constant is correct:

```
const greeting = "Hello!";
```

But this next one definitely causes an error:

```
const greeting; // -> Uncaught SyntaxError: Missing initializer in const declaration
greeting = "Hello";
```

As we said, a change in the constant is impossible. This time the declaration is correct, but we try to modify the value stored in the constant.

```
const greeting = "Hello";
greeting = "Hi!"; // -> Uncaught TypeError: Assignment to constant variable.
```

The main purpose of a constant is to eradicate the possibility of accidentally changing a value stored in it. This is important when we have some values that really should never change. Typical examples of constants are paths to resources, tokens, and other data that never change throughout the lifetime of the script.

But constants can also be used as sub results in calculations or in other places where whatever information was gathered or calculated will not change any further. Using a const, besides preventing a value from being changed by mistake, allows the JavaScript engine to optimize the code, which may affect its performance.

## Scope
