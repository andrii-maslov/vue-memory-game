<template>
  <div class="game-table">
    <GameCell
      v-for="(item, index) in 24"
      :key="item.id"
      :id="index"
      :items="items"
      :shownCards="shownCards"
      :start="start"
      :activeCards="activeCards"
      :itemClosed="itemsClosed"
      @changeShownCards="shownCards++"
      :class="{completed: itemsClosed[index]}"
    >
    </GameCell>
  </div>
</template>

<script>
import GameCell from "./GameCell";
export default {
  name: "Game",
  components: {GameCell},
  data() {
    return {
      items: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24],
      itemsClosed: new Array(24),
      shownCards: 0,
      activeCards: [],
      completedCards: 0,
    }
  },
  props: {
    start: Boolean,
  },
  beforeMount() {
    let tempArray = this.items;
    tempArray.sort(function() { return Math.random() - 0.5});
    tempArray = tempArray.map((item) => {
      return item % 6 + 1;
    });
    this.items = tempArray;
  },
  methods: {
    stopTimer() {
      console.log('stop timer')
      this.$emit('gameStopped', false);
    }
  },
  watch: {
    shownCards() {
      if (this.shownCards > 1) {
        setTimeout(() => {
          this.shownCards = 0;

          let cells = document.querySelectorAll('.game-cell');
          cells.forEach(function(item) {
            item.innerHTML = '';
          });
          // console.log(document.querySelectorAll('.game-cell'))
          console.log('clear')
        }, 1000);
      }
    },
    activeCards() {
      if (this.activeCards.length === 2) {
        if (this.items[this.activeCards[0]] === this.items[this.activeCards[1]]) {
          this.itemsClosed[this.activeCards[0]] = 1;
          this.itemsClosed[this.activeCards[1]] = 1;
          this.completedCards += 2;
        }
        this.activeCards = [];
      }
    },
    completedCards() {
      if (this.completedCards === 4) {

        this.stopTimer();
        // this.start = false;
        console.log('Finish')
      }
    }
  }
}
</script>

<style scoped>
  .game-table {
    width: 650px;
    display: flex;
    flex-wrap: wrap;
  }
</style>
