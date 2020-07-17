# Function Composition

<mark>Function composition is the process of combining two or more functions to produce a new function. Composing functions together is like snapping together a series of pipes for our data to flow through.</mark>

Put simply, a composition of functions `f` and `g` can be defined as `f(g(x))`, which evaluates from the inside out — right to left. In other words, the evaluation order is:

- `x`
- `g`
- `f`

---

Let’s look at this more closely in code. Imagine you want to convert user’s full names to URL slugs to give each of your users a profile page. In order to do that, you need to walk through a series of steps:

1. split the name into an array on spaces
2. map the name to lower case
3. join with dashes
4. encode the URI component

Here’s a simple implementation:

```
const toSlug = input => encodeURIComponent(
  input.split(' ')
    .map(str => str.toLowerCase())
    .join('-')
);
```

Not bad… but what if I told you it could be more readable?

Imagine each of these operations had a corresponding composable function. This could be written as:

```
const toSlug = input => encodeURIComponent(
  join('-')(
    map(toLowerCase)(
      split(' ')(
        input
      )
    )
  )
);

console.log(toSlug('JS Cheerleader')); // 'js-cheerleader'
```

This looks even harder to read than our first attempt, but hang in there, this is going somewhere.
In order to accomplish this, we’re using composable forms of common utilities like `split()`, `join()` and `map()`.

Here are the implementations:

```
const curry = fn => (...args) => fn.bind(null, ...args);

const map = curry((fn, arr) => arr.map(fn));

const join = curry((str, arr) => arr.join(str));

const toLowerCase = str => str.toLowerCase();

const split = curry((splitOn, str) => str.split(splitOn));
```

With the exception of `toLowerCase()`, production-tested versions of all of these functions are available from Lodash/fp. You can import them like this:

```
import { curry, map, join, split } from 'lodash/fp';
```

I’m being a little lazy here. Notice that this curry isn’t technically a real curry, which would always produce a unary function. Instead, it’s a simple partial application. See [“What’s the Difference Between Curry and Partial Application?”](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8), but for the purposes of this demonstration, it will work interchangeably with a real curry function.
Going back to our `toSlug()` implementation, there’s something that really bothers me about it:

```
const toSlug = input => encodeURIComponent(
  join('-')(
    map(toLowerCase)(
      split(' ')(
        input
      )
    )
  )
);

console.log(toSlug('JS Cheerleader')); // 'js-cheerleader'
```

That looks like a lot of nesting to me, and it’s a bit confusing to read. We can flatten the nesting with a function that will compose these functions for us automatically, meaning that it will take the output from one function and automatically patch it to the input of the next function until it spits out the final value.

Come to think of it, we have an array extras utility that sounds like it does something like that. It takes a list of values and applies a function to each of those values, accumulating a single result. The values themselves can be functions. The function is called `reduce()`, but to match the compose behavior above, we need it to reduce right to left, instead of left to right.

Good thing there’s a `reduceRight()` that does exactly what we’re looking for:

```
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);
```

Like `.reduce()`, the array `.reduceRight()` method takes a reducer function and an initial value (`x`). We iterate over the array functions (from right to left), applying each in turn to the accumulated value (`v`).

With compose, we can rewrite our composition above without the nesting:

```
const toSlug = compose(
  encodeURIComponent,
  join('-'),
  map(toLowerCase),
  split(' ')
);

console.log(toSlug('JS Cheerleader')); // 'js-cheerleader'
```

Compose is great when you’re thinking in terms of the mathematical form of composition, inside out… but what if you want to think in terms of the sequence from left to right?

There’s another form commonly called `pipe()`. Lodash calls it `flow()`:

```
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);

const fn1 = s => s.toLowerCase();
const fn2 = s => s.split('').reverse().join('');
const fn3 = s => s + '!'

const newFunc = pipe(fn1, fn2, fn3);
const result = newFunc('Time'); // emit!
```

Notice the implementation is exactly the same as `compose()`, except that we’re using `.reduce()` instead of `.reduceRight()`, which reduces left to right instead of right to left.

Let’s look at our `toSlug()` function implemented with `pipe()`:

```
const toSlug = pipe(
  split(' '),
  map(toLowerCase),
  join('-'),
  encodeURIComponent
);

console.log(toSlug('JS Cheerleader')); // 'js-cheerleader'
```

For me, this is much easier to read.

Hardcore functional programmers define their entire application in terms of function compositions.
I use it frequently to eliminate the need for temporary variables. Look at the `pipe()` version of `toSlug()` carefully and you might notice something special.

In imperative programming, when you’re performing transformations on some variable, you’ll find references to the variable in each step of the transformation. The `pipe()` implementation above is written in a points-free style, which means that it does not identify the arguments on which it operates at all.
I frequently use pipes in things like unit tests and Redux state reducers to eliminate the need for intermediary variables which exist only to hold transient values between one operation and the next.

That may sound weird at first, but as you get practice with it, you’ll find that in functional programming, you’re working with very abstract, generalized functions in which the names of things don’t matter so much. Names just get in the way. You may start to think of variables as unnecessary boilerplate.

That said, I’m of the opinion that points-free style can be taken too far. It can become too dense, and harder to understand, but if you get confused, here’s a little tip… you can tap into the flow to trace what’s going on:

```
const trace = curry((label, x) => {
  console.log(`== ${ label }:  ${ x }`);
  return x;
});
```

Here’s how you use it:

```
const toSlug = pipe(
  trace('input'),
  split(' '),
  map(toLowerCase),
  trace('after map'),
  join('-'),
  encodeURIComponent
);

console.log(toSlug('JS Cheerleader'));
// '== input:  JS Cheerleader'
// '== after map:  js,cheerleader'
// 'js-cheerleader'
```

`trace()` is just a special form of the more general `tap()`, which lets you perform some action for each value that flows through the pipe. Get it? Pipe? Tap? You can write `tap()` like this:

```
const tap = curry((fn, x) => {
  fn(x);
  return x;
});
```

Now you can see how `trace()` is just a special-cased `tap()`:

```
  const trace = label => {
  return tap(x => console.log(`== ${ label }:  ${ x }`));
};
```

You should be starting to get a sense of what functional programming is like, and how partial application & currying collaborate with function composition to help you write programs which are more readable with less boilerplate.

# References

[Master the JavaScript Interview: What is Function Composition?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0)
