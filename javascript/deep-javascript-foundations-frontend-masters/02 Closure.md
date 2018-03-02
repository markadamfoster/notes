# Closure

**Definition**: Closure is when a function remembers and has access to its lexical scope even when the function is executed outside that lexical scope.

```js
function foo() {
  var bar = 'bar'

  function baz() {
    console.log(bar)
  }

  bam(baz)
}

function bam(baz) {
  baz() // "bar"
}

foo()
```

Within bam(), baz() is being executed in an entirely different scope then where it was declared... but it still has access to is lexical scope.

Another example:

```js
function foo() {
  var bar = 'bar'

  setTimeout(function() {
    console.log(bar)
  }, 1000)
}

foo()
```

Closure is how the function within the setTimeout continues to access the bar variable long after foo() has finished executing.

Classic example:

```js
for (var i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log('i: ' + i)
  }, i * 1000)
}
```

This actually logs "i: 6" all 6 times. Why? Because of closure. One `var i` is closed over by all 6 setTimeouts, and it's value is 6 by the time each function fires.

In IIFE would change this:

```js
for (var i = 1; i <= 5; i++) {
  ;(function(i) {
    setTimeout(function() {
      console.log('i: ' + i)
    }, i * 1000)
  })(i)
}
```

With this IIFE pattern, we're closing over the `i` parameter of the function... we're creating a new `i` variable every time the loop runs. This correctly logs the incrementing i value.

Another way to do this... block scoping via `let`:

```js
for (var i = 1; i <= 5; i++) {
  let j = i
  setTimeout(function() {
    console.log('j: ' + j)
  }, j * 1000)
}
```

This creates a new `j` variable with each iteration of the loop. And actually, if you use `let` instead of `var` when creating the loop, you don't need the `let j = i` code:

```js
for (let i = 1; i <= 5; i++) {
  setTimeout(function() {
    console.log('i: ' + i)
  }, i * 1000)
}
```
