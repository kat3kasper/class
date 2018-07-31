# Closures

## Objectives
* Students will be able to explain what a closure in terms of lexical environment
* Students will be able to name 1 common use case for closures

## Why?
Closures are frequently used in JavaScript for object data privacy, in event handlers and callback functions, and in partial applications, currying, and other functional programming patterns.

## Warm Up
With a partner discuss the following for 1 minute:
* What is scope?
* What is the difference between global scope and local scope?

## Closures and Lexical Scoping.. Oh My!

### Scenarios
Take a look at the following 2 examples and try to guess what will be displayed in the console before running the repl.it. Discuss with your partner why you think it works like that.

1. The function `pirateGreeting` uses an external variable `pirate`. When the function runs, which value is it going to use?
```javascript
let pirate = 'Captain Jack Sparrow'

function pirateGreeting() {
  console.log(`Arrrr Matey, me name's ${pirate}`)
}

pirate = 'Will Turner'

pirateGreeting()// Who will greet us? Jack or Will?
```
[Run the repl.it](https://repl.it/@kasperweb/PirateGreeting)

2. The function `makePirateGreeting` makes another function and returns it. That new function can be called later on or from somewhere else. Will it have access to the outer variables from its creation place, or the invocation place, or both?

```javascript
function makePirateGreeting() {
  let pirate = 'Captain Jack Sparrow'
  
  return function() {
    console.log(`Arrrr Matey, me name's ${pirate}`)
  }
}

let pirate = 'Will Turner'

//Create a function
let pirateGreeting = makePirateGreeting()

// Call it
pirateGreeting()// Who will greet us? Jack or Will?
```

[Run the repl.it](https://repl.it/@kasperweb/PirateClosure)

