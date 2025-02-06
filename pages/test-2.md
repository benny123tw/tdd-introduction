---
layout: tdd-demo
transition: none
---

<template v-slot:header>
  <v-switch>
    <template #0>
      <StatusBar :isPass="true" />
    </template>
    <template #2>
      <StatusBar :isPass="false" errorMessage="Expected: 20, Received: 15" />
    </template>
    <template #3-7>
      <StatusBar :isPass="true" />
    </template>
  </v-switch>
</template>

::left::

<code>Game.test.ts</code>

````md magic-move {at:1, lines: true}
```ts{8-9}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

it('1 spare', () => {
  g.roll(5)
  g.roll(5)
  g.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})
```

```ts{*}
// code
function rollSpare() {
  game.roll(5)
  game.roll(5)
}

it('1 spare', () => {
  rollSpare()
  game.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})
```

```ts{*|*|10-11}
// code
it('1 spare', () => {
  rollSpare()
  game.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})

it('1 strike', () => {
  game.roll(10)
  game.roll(2)
  game.roll(3)
  rollMany(16, 0)
  expect(game.score(), 20)
})
```

```ts{*}
// code
function rollStrike() {
  game.roll(10)
}

it('1 strike', () => {
  rollStrike()
  game.roll(2)
  game.roll(3)
  rollMany(16, 0)
  expect(game.score(), 20)
})
```

Write the final test

```ts{*}
// code

it('1 spare', () => {
  // ...
})

it('1 strike', () => {
  // ...
})

it('perfect game', () => {
  rollMany(12, 10)
  expect(game.score(), 300)
})
```

````

::right::

<code>Game.ts</code>

````md magic-move {at:1, lines: true}
Fix the spare test

```ts {7-10}
export class Game {
  // ...
  score(): number {
    let score = 0
    let i = 0
    for (let frame=0; frame<10; frame++) {
      if (this.rolls[i] 
        + this.rolls[i+1] === 10) {
        score += 10 + this.rolls[i+2]
        i += 2
      }
      else {
        score += this.rolls[i] + this.rolls[i+1]
        i += 2
      }
    }
    return score
  }
}
```

```ts {*|*}
  score(): number {
    // ...
    for (let frame=0; frame<10; frame++) {
      if (this.isSpare(i)) {
        score += 10 + this.spareBonus(i)
        i += 2
      }
    // ...
  }

  function isSpare(i: number) {
    return this.rolls[i]
      + this.rolls[i+1] === 10
  }

  function spareBonus(i: number) {
    return this.rolls[i+2]
  }
```

```ts {*|6-10}
export class Game {
  // ...
  score(): number {
    // ...
    for (let frame=0; frame<10; frame++) {
      if (this.rolls[i] === 10) {
        score += 10 
          + this.rolls[i+1] 
          + this.rolls[i+2]
        i += 1
      }
      else if (this.isSpare(i)) {
        score += 10 + this.spareBonus(i)
        i += 2
      }
  // ...
}
```

```ts {*|*|*}
export class Game {
  // ...
  score(): number {
    // ...
    for (let frame=0; frame<10; frame++) {
      if (this.isStrike(i)) {
        score += 10 + this.strikeBonus(i)
        i += 1
      }
      else if (this.isSpare(i)) {
        score += 10 + this.spareBonus(i)
        i += 2
      }
      // ...
    }
    return score
  }
}
```

````