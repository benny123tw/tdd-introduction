<script setup lang="ts">
const props = defineProps({
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
  testResult: {
    type: Boolean,
    required: true,
  }
})
</script>

<template>
  <slot name="header" />
  <div class="slidev-layout two-columns w-full h-full grid grid-cols-2 items-start gap-4" :class="props.layoutClass">
    <div class="col-left" :class="props.class">
      <slot name="left" />
    </div>
    <div class="col-right" :class="props.class">
      <slot name="right" />
    </div>
  </div>
</template>