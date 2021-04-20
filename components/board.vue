<template>
  <div
    class="flex flex-col rounded-lg box-content backdrop-filter backdrop-invert shadow-xl"
  >
    <div v-for="row in rows" :key="row" class="flex">
      <cell
        v-for="column in columns"
        :key="`${row}${column}`"
        :index="(row - 1) * rows + column"
        :piece="pieces[row - 1][column - 1]"
        :is-black="column % 2 !== row % 2"
        :tl="row == 1 && column == 1"
        :tr="row == 1 && column == columns"
        :bl="row == rows && column == 1"
        :br="row == rows && column == columns"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    columns: 8,
    rows: 8,
    pieces: [
      ['bR', 'bN', 'bB', 'bQ', 'bK', 'bB', 'bN', 'bR'],
      ['bP', 'bP', 'bP', 'bP', 'bP', 'bP', 'bP', 'bP'],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['wP', 'wP', 'wP', 'wP', 'wP', 'wP', 'wP', 'wP'],
      ['wR', 'wN', 'wB', 'wQ', 'wK', 'wB', 'wN', 'wR'],
    ],
  }),
}
</script>
