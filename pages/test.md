---
layout: tdd-demo
transition: none
---

<template v-slot:header>
  <v-switch>
    <template #0-2>
      <StatusBar :isPass="false" errorMessage="ReferenceError: Can't find variable: Game" />
    </template>
    <template #2-3>
      <StatusBar :isPass="true" />
    </template>
    <template #3>
      <StatusBar :isPass="false" errorMessage="TypeError: game.roll is not a function." />
    </template>
    <template #4>
      <StatusBar :isPass="false" errorMessage="Expected: 0, Received: -1" />
    </template>
    <template #5>
      <StatusBar :isPass="true" />
    </template>
    <template #7>
      <StatusBar :isPass="false" errorMessage="Expected: 20, Received: 0" />
    </template>
    <template #8>
      <StatusBar :isPass="true" />
    </template>
    <template #10>
      <StatusBar :isPass="false" errorMessage="Expected: 16, Received: 13" />
    </template>
    <template #11>
      <StatusBar :isPass="true" />
    </template>
    <template #12>
      <StatusBar :isPass="false" errorMessage="Expected: 16, Received: 13" />
    </template>
    <template #13>
      <StatusBar :isPass="true" />
    </template>
    <template #14>
      <StatusBar :isPass="false" errorMessage="Expected: 16, Received: 13" />
    </template>
    <template #15>
      <StatusBar :isPass="true" />
    </template>
  </v-switch>
</template>

::left::

<code>Game.test.ts</code>

````md magic-move {at:1, lines: true}
```ts {*|5}
import { describe, it } from 'bun:test'

describe('Bowling Game Kata', () => {
  it('can create the game', () => {
    const game = new Game()
  })
})
```

Error: Game is not defined

```ts {*} 
import { describe, it } from 'bun:test'
import { Game } from '@/Game'

describe('Bowling Game Kata', () => {
  it('can create the game', () => {
    const game = new Game()
  })
})
```

```ts {*|12,15|*} 
// import codes...

describe('Bowling Game Kata', () => {
  it('can create the game', () => {
    const game = new Game()
  })

  it('all gutters game', () => {
    const game = new Game()

    for (let i = 0; i < 20; i++) {
      game.roll(0)
    }

    expect(game.score(), 0)
  })
})
```

Refactor the code

```ts{*}
// import codes...

describe('Bowling Game Kata', () => {
  let game: Game

  beforeEach(() => {
    game = new Game()
  })

  it('all gutters game', () => {
    for (let i = 0; i < 20; i++) {
      game.roll(0)
    }

    expect(game.score(), 0)
  })
})
```

Write a failing test

```ts{*|*}
// code
it('all gutters game', () => {
  for (let i = 0; i < 20; i++) {
    game.roll(0)
  }

  expect(game.score(), 0)
})

it('all one game', () => {
  for (let i = 0; i < 20; i++) {
    game.roll(1)
  }

  expect(game.score(), 20)
})
```

Refactor the test

```ts{*}
// code
function rollMany(n: number, pins: number) {
  for (let i = 0; i < n; i++) {
    game.roll(pins)
  }
}

it('all gutters game', () => {
  rollMany(20, 0)
  expect(game.score(), 0)
})

it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})
```

Write a failing test

```ts{*}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

it('1 spare', () => {
  game.roll(5)
  game.roll(5)
  game.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})
```

Design goes wrong, ignore the spare test and refactor

```ts{*}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

// it('1 spare', () => {
//   game.roll(5)
//   game.roll(5)
//   game.roll(3)
//   rollMany(17, 0)
//   expect(game.score(), 16)
// })
```

Try to solve the spare test

```ts{*}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

it('1 spare', () => {
  game.roll(5)
  game.roll(5)
  game.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})
```

Still has some design issues

```ts{*}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

// it('1 spare', () => {
//   game.roll(5)
//   game.roll(5)
//   game.roll(3)
//   rollMany(17, 0)
//   expect(game.score(), 16)
// })
```

Use the correct design and fix the spare test

```ts{*|*}
// code
it('all one game', () => {
  rollMany(20, 1)
  expect(game.score(), 20)
})

it('1 spare', () => {
  game.roll(5)
  game.roll(5)
  game.roll(3)
  rollMany(17, 0)
  expect(game.score(), 16)
})
```

````

::right::

<code>Game.ts</code>

````md magic-move {at:2, lines: true}
```ts {*}
// empty file
```

```ts {*|*}
export class Game {}
```

```ts {*}
export class Game {
  roll(pins: number) {

  }

  score(): number {
    return -1
  }
}
```

```ts {*|*|*}
export class Game {
  roll(pins: number) {

  }

  score(): number {
    return 0
  }
}
```

```ts {*|*|*}
export class Game {
  private _score: number = 0

  roll(pins: number) {
    this._score += pins
  }

  score(): number {
    return this._score
  }
}
```

Refactor the methods roll and score

```ts {*}
export class Game {
  private rolls: number[] = 
    Array.from({ length: 21 }, () => 0)
  private currentRoll = 0

  roll(pins: number) {
    this.rolls[this.currentRoll++] = pins
  }

  score(): number {
    let score = 0
    for (let i=0; i<this.roll.length; i++) {
      score += this.rolls[i]
    }
    return score
  }
}
```

Fix the test

```ts {10-13}
export class Game {
  // code...
  roll(pins: number) {
    this.rolls[this.currentRoll++] = pins
  }

  score(): number {
    let score = 0
    for (let i=0; i<this.roll.length; i++) {
      if (this.rolls[i] 
        + this.rolls[i+1] === 10)
        // ...
        // design is still wrong.
      score += this.rolls[i]
    }
    return score
  }
}
```

Use the correct design

```ts {*|*}
export class Game {
  // ...
  score(): number {
    let score = 0
    let i = 0
    for (let frame=0; frame<10; frame++) {
      score += this.rolls[i] + this.rolls[i+1]
      i += 2
    }
    return score
  }
}
```

Fix the spare test

```ts {*}
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

````

---
src: ./test-2.md
---