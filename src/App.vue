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
          v-on:click="openTile(tile)"
          v-on:contextmenu.prevent="flagTile(tile)"
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
    },

    showAll: function() {
      /**
       * Shows all board tiles
       *
       * @return undefined
       */
      // 開いていない、tileを全部開いて回答を見せる
      this.tiles.forEach(row => {
        row.forEach(tile => {
          this.openTile(tile, true);
        });
      });
    },

    openTile: function(tile, allOpen) {
      /**
       * @param tile Tile object
       * @param allOpen showAllから呼ばれるときだけtrueにする、など
       *                それ以外から呼ばれるとき、allOpenを指定しなければ、undefinedになるので、
       *                falseと同じように扱うことができる、はず
       *
       * @return undefined
       */

      if (tile.mined) {
        // ここにはいるのは、ユーザがクリックしたタイルがmineであるときのみ！
        tile.state = ['mine'];
        if (!allOpen) {
          this.showAll();
        }
        return;
      }

      // 処理効率を考えると、minedの判定をした後の方がよい
      let neighbors = this.getNeighbors(tile);
      let neighborMineCount = this.countNeighboringMines(neighbors);

      if (neighborMineCount) {
        // 再帰呼出については必ずここで終わる
        tile.state = ['mine-neighbour-' + neighborMineCount];
      } else {
        tile.state = ['opened'];
        if (!allOpen) {
          // neighborsは全部minedではない！
          neighbors.forEach(neighbor => {
            if (this.isUnopened(neighbor)) {
              this.openTile(neighbor); // openTileを呼んでも、L74の条件には絶対に引っかからない
            }
          });
        }
      }
    },

    flagTile: function(tile) {
      /**
       * @param tile tile object
       *
       * @return undefined
       */
      if (tile.state[0] === 'flagged') {
        tile.state = ['unopened'];
      } else {
        tile.state = ['flagged'];
      }
    },

    getNeighbors: function(tile) {
      /**
       * @param tile tile object
       *
       * @return Array<tile objects>
       */
      const { row, col } = tile;
      let neighborIndices = [
        [row - 1, col - 1], [row - 1, col], [row - 1, col + 1],
        [row, col - 1],                     [row, col + 1],
        [row + 1, col - 1], [row + 1, col], [row + 1, col + 1]
      ];

      return neighborIndices
        .filter(([row, col]) => this.isValid(row, col)) // 囲むtileのrow/colがボード外だったら配列から削除する
        .map(([row, col]) => this.tiles[row][col]); // row/col数をタイルオブジェクトに変換する
    },

    countNeighboringMines: function(neighbors) {
      /**
       * @param neighbors Array<tile objects>
       *
       * @return number
       */
      return neighbors.filter(neighbor => neighbor.mined).length;
    },

    isUnopened: function(tile) {
      /**
       * @param tile tile object
       *
       * @return boolean
       */
      return tile.state[0] === 'unopened';
    },

    isValid: function(row, col) {
      /**
       * @param row number
       * @param col number
       *
       * Checks to see if row and col are valid indices (within the game board boundaries)
       *
       * @return boolean
       */
      return (row >= 0 && row < this.tiles.length) &&
             (col >= 0 && col < this.tiles[0].length);
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
