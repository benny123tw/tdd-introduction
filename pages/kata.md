---
title: 'Kata'
---

![Scoring Bowling](/scores.png)

<!--
The game consists of 10 frames as shown above.  In each frame the player has
two opportunities to knock down 10 pins.  The score for the frame is the total
number of pins knocked down, plus bonuses for strikes and spares.

A spare is when the player knocks down all 10 pins in two tries.  The bonus for
that frame is the number of pins knocked down by the next roll.  So in frame 3
above, the score is 10 (the total number knocked down) plus a bonus of 5 (the
number of pins knocked down on the next roll.)

A strike is when the player knocks down all 10 pins on his first try.  The bonus
for that frame is the value of the next two balls rolled.

In the tenth frame a player who rolls a spare or strike is allowed to roll the extra
balls to complete the frame.  However no more than three balls can be rolled in
tenth frame.
-->

---
title: 'Requirements'
---

## Requirements

```mermaid
classDiagram
    class Game {
        +roll(pins: number)
        +score() number
    }
```

Write a class named <span text-orange v-mark="{at: 1, color: 'orange', type: 'circle'}">`Game`</span> that has two methods
<span text-orange v-mark="{at: 1, color: 'orange', type: 'circle'}">`roll(pins: number)`</span> is called each time the player rolls a ball. The argument is the number of pins knocked down. <br>
<span text-orange v-mark="{at: 1, color: 'orange', type: 'circle'}">`score(): number`</span> is called only at the very end of the game.  It returns the total score for that game.

---
layout: center
---

<v-switch text-center>
<template #0>

```mermaid
classDiagram
    class Game {
        +roll(pins: number)
        +score() number
    }
```

Clearly, we need the <span text-orange>`Game`</span> class.
</template>

<template #1>
```mermaid
---
config:
  class:
    hideEmptyMembersBox: true
---

classDiagram
direction LR
    class Game {
        +roll(pins: number)
        +score() number
    }

    class Frame {
    }

    Game "1" --> "10" Frame
```

A game has 10 frames.
</template>

<template #2>
```mermaid
---
config:
  class:
    hideEmptyMembersBox: true
---

classDiagram
direction LR
    class Game {
        +roll(pins: number)
        +score() number
    }

    class Frame {
    }

    class Roll {
        -pins: number
    }

    Game "1" --> "10" Frame
    Frame "1" --> "1..2" Roll
```

A frame has 1 or two rolls.

</template>
<template #3>
```mermaid
---
config:
  class:
    hideEmptyMembersBox: true
---

classDiagram
direction LR
    class Game {
        +roll(pins: number)
        +score() number
    }

    class Frame {
    }

    class Roll {
        -pins: number
    }

    class TenthFrame {
    }

    Game "1" --> "10" Frame
    Frame "1" --> "1..2" Roll
    Frame <|-- TenthFrame
    TenthFrame "1" --> "1" Roll
```

The score function must iterate through all the frames, and calculate all their scores.
</template>

<template #4>
```mermaid
---
config:
  class:
    hideEmptyMembersBox: true
---

classDiagram
direction LR
    class Game {
        +roll(pins: number)
        +score() number
    }

    class Frame {
        +score() number
    }

    class Roll {
        -pins: number
    }

    class TenthFrame {
    }

    Game "1" --> "10" Frame
    Frame "1" --> "1..2" Roll
    Frame <|-- TenthFrame
    TenthFrame "1" --> "1" Roll
    Frame --> Frame : next frame
```

The score for a spare or a strike depends on the frame’s successor
</template>
</v-switch>