# Pure Function

## What is a Function?

A **function** is a process which takes some input, called **arguments**, and produces some output called a **return value**. Functions may serve the following purposes:

- **Mapping:** Produce some output based on given inputs. A function maps input values to output values.
- **Procedures:** A function may be called to perform a sequence of steps. The sequence is known as a procedure, and programming in this style is known as procedural programming.
- **I/O:** Some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network.

## Pure functions

Pure Functions are functions which obey two laws:

- **Given the same input, always return the same output**
- **Produce no side-effects**

The functional programming paradigm uses pure functions as the primary unit of composition: the fundamental building block we build our applications with.

Not all functions in JavaScript can be pure, but when they can, it's often a good choice. Using an impure function where a pure function is required is a common source of bugs. For instance, React and Redux reducer functions must be pure in order to ensure that your UI compenents render properly.

### Mapping

Functions map input arguments to return values, meaning that for each set of inputs, there exists an output. A function will take the inputs and return the corresponding output.

`Math.max()` takes numbers as arguments and returns the largest number:

```
Math.max(2, 8, 5); // => 8
```

In this example, 2, 8, & 5 are arguments. They’re values passed into the function.

`Math.max()` is a function that takes any number of arguments and returns the largest argument value. In this case, the largest number we passed in was 8, and that’s the number that got returned.

### Links

[Medium - pure function](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)
[Lesson - pure function](https://ericelliottjs.com/premium-content/lesson-pure-functions)
