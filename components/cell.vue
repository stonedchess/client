<template>
  <div
    class="w-20 h-20 flex items-center justify-center bg-gray-50"
    :class="{
      'bg-opacity-70': isBlack,
      'bg-opacity-10': !isBlack,
      'rounded-tl': tl,
      'rounded-tr': tr,
      'rounded-bl': bl,
      'rounded-br': br,
      'cursor-move': piece !== '',
    }"
  >
    <img
      v-if="piece !== ''"
      :src="require(`~/assets/pieces/riohacha/${piece}.svg`)"
      class="w-3/4"
    />
  </div>
</template>

<script>
export default {
  props: {
    index: { type: Number, required: true },
    piece: { type: String, required: true },
    isBlack: { type: Boolean, required: true },
    tl: { type: Boolean, required: true },
    tr: { type: Boolean, required: true },
    bl: { type: Boolean, required: true },
    br: { type: Boolean, required: true },
  },
}
</script>
