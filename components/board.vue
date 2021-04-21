<template>
  <div class="relative">
    <div
      class="grid rounded backdrop-filter backdrop-invert shadow-xl"
      :class="`grid-cols-${columns} grid-rows-${rows}`"
    >
      <cell
        v-for="(cell, index) in cells"
        :key="index"
        :corner-tl="index === 0"
        :corner-tr="index === 7"
        :corner-bl="index === 56"
        :corner-br="index === 63"
        v-bind="cell"
        @click="onCellClick"
      />
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    columns: 8,
    rows: 8,
    cells: [
      ['bR', 'bN', 'bB', 'bQ', 'bK', 'bB', 'bN', 'bR'],
      ['bP', 'bP', 'bP', 'bP', 'bP', 'bP', 'bP', 'bP'],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['', '', '', '', '', '', '', ''],
      ['wP', 'wP', 'wP', 'wP', 'wP', 'wP', 'wP', 'wP'],
      ['wR', 'wN', 'wB', 'wQ', 'wK', 'wB', 'wN', 'wR'],
    ]
      .flat()
      .map((piece, index) => {
        const file = index % 8
        const rank = Math.floor(index / 8)
        const black = rank % 2 !== file % 2
        return { piece, file, rank, black, selected: false }
      }),
    selected: undefined,
  }),
  methods: {
    onCellClick(rank, file) {
      const cell = this.cells[rank * 8 + file]

      if (this.selected === undefined || this.selected.piece === '') {
        if (cell.piece !== '') {
          this.selected = cell
          this.selected.selected = true
        }
      } else {
        if (rank !== this.selected.rank || file !== this.selected.file) {
          cell.piece = this.selected.piece
          this.selected.piece = ''
        }
        this.selected.selected = false
        this.selected = undefined
      }
    },
  },
}
</script>
