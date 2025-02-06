<template>
    <div class="w-full flex justify-center mb-4">
        <div :class="isPass ? 'bg-green-500' : 'bg-red-500'" class="w-1/2 h-8 flex items-center justify-center">
            <span class="text-white text-2xl">{{ errorMessage }}</span>
        </div>
    </div>
</template>
  
<script>
  import { defineComponent, toRefs } from 'vue';
  
  export default defineComponent({
    name: 'StatusBar',
    props: {
      isPass: {
        type: Boolean,
        required: true
      },
      errorMessage: {
        type: String,
      }
    },
    setup(props) {
      const { isPass, errorMessage } = toRefs(props);
      return { isPass, errorMessage };
    }
  });
</script>
  
<style scoped>
</style>