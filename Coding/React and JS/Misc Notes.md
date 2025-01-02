## Closures

- when function in another function it creates a closure
- a closure is the inner function in combination with the environment in which it was created
### Hooks and Closures
- useState(x) will create a closure where the state variable is in the environment and return 

## Map
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map
- "The `Map` object holds key-value pairs and remembers the original insertion order of the keys"
- can get keys with .keys(), which gives iterable object. can use .next(), to get first element, then 2nd on next call of next(), etc