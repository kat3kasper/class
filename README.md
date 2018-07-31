# Closures

## Objectives

```javascript
function makePirateGreeting() {
  let pirate = 'Captain Jack Sparrow'
    return function() {
    console.log(`Arrrr Matey, me name's ${pirate}`)
  }
}

let pirate = 'Will Turner'

let pirateGreeting = makePirateGreeting()
pirateGreeting()// Who will greet us? Jack or Will?
```
