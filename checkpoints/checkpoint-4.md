# チェックポイント４（５日目）

テックメンターが下記の項目を行います：

* [ ] Solution walkthrough - `flagTile` solution code
  * [ ] Solution walkthrough - `v-on:contextmenu.prevent` on each tile
* [ ] Solution walkthrough - `countNeighboringMines` solution code
* [ ] Solution walkthrough - the `openTile` method (explain what it is recursively doing)
  * [ ] Note: We attached a click handler to the tile to invoke `openTile`.

下記の項目を実装してみよう：

* [ ] `showAll` method
  * [ ] Be careful! We want to reuse openTile for the showAll method, but we don't want to infinitely recurse. Can you figure out how?
  * Hint: You will need to give an extra argument to openTile.