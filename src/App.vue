<template>
  <div id="app">
    <button v-on:click="startGame">Start Game</button>
    <table class="minesweeper">
      <tr
        v-for="(row, r) in tiles"
        v-bind:key="r"
      >
        <td
          v-for="(tile, c) in row"
          v-bind:key="c"
          v-bind:class="tile.state"
        >
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => {
    return {
      rows: 10,
      columns: 20,
      tiles: [],
    };
  },
  methods: {
    startGame: function() {
      this.tiles = [];
      for (let i = 0; i < this.rows; i++) {
        const row = [];
        for (let j = 0; j < this.columns; j++) {
          let tile = {
            row: i,
            col: j,
            mined: Math.random() * 6 > 5,
            state: ['unopened']
          };
          row.push(tile);
        }
        this.tiles.push(row);
      }
    }
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
  background: #333;
  color: #fff;
}

#app button {
  display: block;
  margin: 50px auto;
}

table.minesweeper {
  margin: auto;
  border: 1px solid #999;
  border-collapse: collapse;
  background-color: #ddd;
}

table.minesweeper td {
  width: 24px;
  height: 24px;
  background-size: cover;
}

td.unopened {
  background: url('./assets/unopened.svg');
  cursor: pointer;
}

td.opened {
  background: url('./assets/opened.svg');
}

td.flagged {
  background: url('./assets/flag.svg');
  cursor: pointer;
}

td.mine {
  background: url('./assets/mine.png');
}

td.mine-neighbour-1 {
  background: url('./assets/1.svg');
}

td.mine-neighbour-2 {
  background: url('./assets/2.svg');
}

td.mine-neighbour-3 {
  background: url('./assets/3.svg');
}

td.mine-neighbour-4 {
  background: url('./assets/4.svg');
}

td.mine-neighbour-5 {
  background: url('./assets/5.svg');
}

td.mine-neighbour-6 {
  background: url('./assets/6.svg');
}

td.mine-neighbour-7 {
  background: url('./assets/7.svg');
}

td.mine-neighbour-8 {
  background: url('./assets/8.svg');
}
</style>
