<template>
  <div
    class="w-20 h-20 flex items-center justify-center"
    :class="{ 'bg-black text-white': isBlack }"
  ></div>
</template>

<script>
export default {
  props: {
    index: { type: Number, required: true },
    isBlack: { type: Boolean, required: true },
  },
}
</script>
