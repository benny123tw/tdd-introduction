---
# You can also start simply with 'default'
theme: eloc
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: "TDD in Bowling Game Kata"
info: |
  ## TDD introduction
  Test first, code less.

# apply unocss classes to the current slide
# class: text-center

# https://sli.dev/features/drawing
drawings:
  persist: false

# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left

fonts:
  sans: Noto Sans TC
# enable MDC Syntax: https://sli.dev/features/mdc
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

<div class="absolute text-gray bottom-10 right-0">
  <span class="font-500 text-md">
    Benny 02/07/2025
  </span>
</div>

---
hideInToc: true
---

# Table of Contents

<Toc maxDepth="1"></Toc>

---
src: ./pages/hook.md
---

---
src: ./pages/introduction.md
---

---
src: ./pages/tdd.md
---

---

#### "Talk is cheap. <br />Show me the code."
_- Linus Torvalds_

---
src: ./pages/demo.md
---
