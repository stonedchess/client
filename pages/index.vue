<template>
  <div class="flex flex-col">
    <div v-for="row in rows" :key="row" class="flex">
      <cell
        v-for="column in columns"
        :key="index(row, column)"
        :index="index(row, column)"
        :is-black="isBlack(row, column)"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    columns: 8,
    rows: 8,
  }),
  methods: {
    index(row, column) {
      return (row - 1) * this.rows + column
    },
    isBlack(row, column) {
      return column % 2 !== row % 2
    },
  },
}
</script>
