# Undefined Coalescing Operator

This is a proposal for introducing a Undefined Coalescing [(Null Coalescing Operator in C#)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-conditional-operator) operator in [ECMAScript](https://github.com/tc39/ecma262/)).

## Motivation

We often provide default values using the logical or operator `||`, for convenience.

```js
var name = user.name || 'Bob'
var bio = user.bio || 'Nothing to see here!'
```

Sometimes, however, the falsy check gets in the way. Particularly for those cases where the value is `''` or `0`, in which case we often want to preserve those values.

```js
var spellWand = {
  remaining: 0
}
console.log(spellWand.remaining || 5) // <- 5
```

When the left-hand side value is `undefined`, the Undefined Coalescing Operator returns the right-hand side value.

```js
var user = {}
console.log(user.name ?? 'Bob') // 'Bob'
```

The Undefined Coalescing Operator returns the left-hand side value in all other cases.

```js
var spellWand = {
  remaining: 0
}
console.log(spellWand.remaining ?? 5) // <- 0
```

## Implementation

`left ?? right` is equivalent to `left === undefined ? right : left`.

## Limitations

C# coalesces `null`, they however don't have a concept for `undefined`. In JavaScript `null` is often treated as interchangeable with `undefined`, but sometimes it's not. Under the current proposal, `null` is not covered by the Undefined Coalescing Operator, and `left === null ? right : left` should still be used for this case.
