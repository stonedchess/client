<template>
  <div class="relative">
    <div
      v-if="id !== undefined"
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
    id: undefined,
    winner: 2,
    player: 1,
    moves: [],
  }),
  async fetch() {
    const res = await fetch('http://127.0.0.1:5000/init')
    const { id } = await res.json()
    this.id = id
  },
  methods: {
    async onCellClick(rank, file) {
      if (this.winner !== 2) return
      const cell = this.cells[rank * 8 + file]

      if (this.selected === undefined || this.selected.piece === '') {
        if (cell.piece !== '') {
          const uri = `http://127.0.0.1:5000/${this.id}/moves/${file}/${rank}`
          const { moves, player } = await fetch(uri).then((res) => res.json())
          if (player === this.player) {
            this.moves = moves
            this.selected = cell
            this.selected.selected = true
          }
        }
      } else {
        const moves = this.moves.filter(
          ({ destination: d }) => d.file === file && d.rank === rank
        )

        if (moves.length > 0) {
          const { origin } = moves[0]
          const uri = `http://127.0.0.1:5000/${this.id}/move/${origin.file}/${origin.rank}/${file}/${rank}`
          await fetch(uri)
            .then((res) => res.json())
            .then(({ winner }) => (this.winner = winner))
            .then(() => {
              cell.piece = this.selected.piece
              this.player = 1 - this.player
              this.selected.piece = ''
            })
        }

        this.selected.selected = false
        this.selected = undefined
        this.moves = []
      }
    },
  },
}
</script>
