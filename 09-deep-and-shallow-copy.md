## Shallow Copy
A shallow copy creates a new object, but nested objects or arrays still point to the same memory location as the original. If you change a nested property in the copy, the original also changes.

- Spread Operator
  `const copy = {...original}`
- Object.assign
  `const copy = Object.assign({},original)`

## Deep Copy
A deep copy creates a completely independent version of the object. Every level of the object is copied into a new memory location. Changing any value in the copy will not affect the original.

- modern approach
  `const copy = structuredClone(original)`
