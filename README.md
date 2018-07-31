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

### Closures

> A closure is the combination of a function and the lexical environment within which that function was declared. 

The term 'closures' is not something only unique to Javascript. [Closure](https://en.wikipedia.org/wiki/Closure_(computer_programming)) are a record storing a function together with its environment.

In Javascript, the environment consists of any local variables that were in-scope at the time the closure was created.

#### Check - What is Lexical Environment?

Everytime a function runs, a new lexical enviroment gets created. In JavaScript, every running function, code block, and the script as a whole have an associated object known as the Lexical Environment.

The lexical environment consists of 2 parts:
1. The Environment Record - object that contains of the local variables as its properties
2. Reference to the outer lexical environment(think of a pointer) - which is typically right outside of the current set of `{}`

#### Examples

##### Data Privacy / Keeping State

```javascript
function makeTreasureCounter() {
  let totalTreasure = 0;
  return function() {
    return ++totalTreasure;
  }
}

let treasureCounter = makeTreasureCounter();

console.log(treasureCounter.totalTreasure) // undefined
console.log(treasureCounter()) // 1
console.log(treasureCounter()) // 2
```

##### Function Factory

```javascript
function treasureMultiplier(multiplier){
  return function(treasure) {
    return multiplier * treasure;
  }
}

let multiplyMeTreasure = treasureMultiplier(1);
let multiplyMeTreasureBy5 = treasureMultiplier(5);

console.log(multiplyMeTreasure(100));
console.log(multiplyMeTreasureBy5(100));
```
[Play](https://repl.it/@kasperweb/FunctionFactory)

#### Singleton / Module

```
pirateTracker = (function() {
  let totalTreasure = 0
  let pirateArray = []

  //pirare = {name,treasure}
  function addPirate(pirate) { 
    totalTreasure += pirate.treasure;
    pirateArray.push(pirate)
  }

  function getTreasure() {
    return totalTreasure;
  }

  return {
    addPirate, getTreasure
  }
})();

pirateTracker.addPirate({name: 'will', treasure: 100})
pirateTracker.addPirate({name: 'jack', treasure: 200})

console.log(pirateTracker.totalTreasure) // undefined
console.log(pirateTracker.getTreasure()) // 300
```
[Play](https://repl.it/@kasperweb/SingletonPirateTracker)

### Your Turn

1. Write function sum that works like this: subtract(a)(b) = a-b

```javascript
subtract(9)(5) = 4
subtract(-3)(2) = -5
```

2.  We are making 2 treasure counters. Do they act independently? What will be logged to the console? 
```javascript
function makeTreasureCounter() {
  let totalTreasure = 0;
  return function() {
    return ++totalTreasure;
  }
}

let willsTreasureCounter = makeTreasureCounter();
let jacksTreasureCounter = makeTreasureCounter();

console.log(treasureCounter.totalTreasure) // undefined
console.log(willsTreasureCounter())
console.log(willsTreasureCounter())

console.log(jacksTreasureCounter())
console.log(jacksTreasureCounter())
```
[Try it out](https://repl.it/@kasperweb/MultipleTreasureCounters)

### Further Readings

[MDN Docs for Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
[Javascript.info)(https://javascript.info/closure)
[Eric Elliott's Master the JS Interview: What is a closure?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)

