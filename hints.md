# TDD Bowling Kata

### Process

- **Start with a test (`Game.test.ts`):**
  - Create an initial test `should create the game.`
  - The test fails due to an unknown variable.

- **Create the Game class in `Game.ts`:**
  - Now the test should pass.

- **Create another test that specifies an "all gutters" game:**
  - The test fails because of an unknown method name.

- **Add `roll` and `score` methods to `Game.ts`:**
  - `roll` should accept a variable `pins` of type number.
  - `score` returns 0 to satisfy the test requirement.
  - Now the test should pass.

- **Refactor the test:**
  - Move `game` to the top.
  - Initialize the game in the `beforeEach` hook.

- **Create a new test case for an "all ones" game:**
  - Roll 20 times with 1 pin.
  - Assert that the score equals 20.
  - The test fails with the wrong assertion (expected 20, received 0).

- **Fix `Game.ts`:**
  - Create a private variable `score`.
  - Add to the `score` each time the user rolls.
  - The method `score` returns the private variable `score`.
  - Now the test should pass.

- **Refactor the test file:**
  - Both the "all gutters game" and "all ones game" use a for loop to roll.
  - Extract the for loop into a function `rollMany` that accepts two parameters: `n` and `pins`.

- **Create a new test case for a "1 spare" game:**
  - Roll 5 pins twice and roll the remaining (17) times with 0 pins.
  - Assert that the score equals 24 (10 + 7 + 7).
  - The test fails with the wrong assertion (expected 24, received 17).

- **Fix `Game.ts`:**
  - Try to add some condition checks in the `roll` method.
  - Realize that this approach violates the "Single Responsibility Principle."
  - Refactor the methods `score` and `roll`:
    - Create a private array `rolls` to store each roll.
    - In TypeScript, you can use an empty array and dynamically push each roll to it.
    - Sum each roll in the `score` method.
  - The spare test should still fail.
  - Consider adding checks to determine whether the sum of the current roll and the next roll is 10, and also check whether the index is odd.
  - Suddenly, you realize this is not a good design:
    - Loop by `frames` instead of by `rolls`.
    - Loop from 0 to 10 frames.
    - Still, you need to count the roll index. Therefore, create a variable `i` to track the roll index.
    - The score should include the current roll plus the next roll.
    - When the sum of the current roll and the next roll is 10, also add the score of the roll after that.
    - The index should increase by 2 each frame.
  - Now the test should pass.

- **Refactor `Game.ts` and `Game.test.ts`:**
  - Extract the spare check into an `isSpare` function.
  - Rename `i` to `rollIndex` for clarity.
  - Extract the two rolls of 5 pins each into a `rollSpare` function.

- **Create a new test case for a "1 strike" game:**
  - Roll 10 pins once, then roll 2 and 3, and then roll the remaining (16) times with 0 pins.
  - Assert that the score equals 20.
  - The test fails with the wrong assertion (expected 20, received 15).

- **Fix `Game.ts`:**
  - Add a check to see if the current roll equals 10.
  - When the current roll is a strike, add the scores of the next two rolls.
  - Increase the roll index by 1 for a strike.
  - Now the test should pass.

- **Refactor `Game.ts` and `Game.test.ts`:**
  - Extract the strike check into an `isStrike` function.
  - Extract the bonus calculations for spares and strikes into methods `spareBonus` and `strikeBonus`.
  - Extract `roll(10)` into a `rollStrike` function.

- **Create a new test case for a "perfect game":**
  - Roll 10 pins 12 times.
  - Assert that the score is equal to 300.
  - The test should pass!

---
