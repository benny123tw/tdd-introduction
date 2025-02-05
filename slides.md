---
theme: eloc
title: "TDD in the Bowling Game Kata - Benny Yen"
info: |
  ## TDD introduction
  Test first, code less.
drawings:
  persist: false
transition: slide-left
fonts:
  # basically the text
  sans: Robot, Noto Sans TC
  # use with `font-serif` css class from UnoCSS
  serif: Robot Slab
  # for code blocks, inline code, etc.
  mono: Fira Code
mdc: true
colorSchema: light
highlighter: shiki

hideInToc: true
---

<h3 bg-gradient-to-r from-blue-600 via-green-500 to-indigo-400 inline-block text-transparent bg-clip-text>From Gutter to Great:<br />
  <span color-gray italic>
    <span color-orange>TDD</span> in the <span color-orange v-mark="{at: 1, color: 'orange', type: 'underline'}">Bowling Game Kata</span>
  </span>
</h3>

<div class="absolute text-gray bottom-10 right-10">
  <span class="font-500 text-md">
    Benny 02/07/2025
  </span>
</div>

<!--
Today, we will be exploring the principles and practices of Test-Driven Development (TDD) using the Bowling Game Kata as a practical example.
-->

---
hideInToc: true
---

#### Table of Contents

<Toc maxDepth="1"></Toc>

---
src: ./pages/hook.md
---

---
src: ./pages/tdd.md
---

---
src: ./pages/kata.md
---

---

#### "Talk is cheap. <br />Show me the code."
_- Linus Torvalds_

---
src: ./pages/demo.md
---

---

<div class="w-60 relative">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-square.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-circle.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-triangle.png"
      alt=""
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    Slidev
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 30, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

[Slide Repo Link](https://github.com/benny123tw/tdd-introduction)

</div>
