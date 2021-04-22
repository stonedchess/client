<template>
  <div
    class="w-20 h-20 flex items-center justify-center bg-opacity-75"
    :class="{
      'bg-gray-50': black,
      'bg-gray-500': !black,
      'rounded-tl': cornerTl,
      'rounded-tr': cornerTr,
      'rounded-bl': cornerBl,
      'rounded-br': cornerBr,
      'cursor-pointer': piece !== '',
      'ring-inset ring-8 ring-white': selected,
    }"
    @click="$emit('click', rank, file)"
  >
    <img
      v-if="piece !== ''"
      class="m-2 pointer-events-none select-none"
      :src="require(`~/assets/pieces/riohacha/${piece}.svg`)"
      :alt="piece"
    />
  </div>
</template>

<script>
export default {
  props: {
    rank: { type: Number, required: true },
    file: { type: Number, required: true },
    piece: { type: String, required: true },
    cornerTl: Boolean,
    cornerTr: Boolean,
    cornerBl: Boolean,
    cornerBr: Boolean,
    black: Boolean,
    selected: Boolean,
  },
  methods: {
    bg() {
      const img = require(`~/assets/pieces/riohacha/${this.piece}.svg`)
      return `background-image: url(${img});`
    },
  },
}
</script>
