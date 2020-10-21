<template>
  <div
    class="game-cell"
    @click="clickOnCell"
  >
  </div>
</template>

<script>
export default {
  name: "GameCell",
  data() {
    return {
      openCards: 0,
    }
  },
  props: {
    index: Number,
    items: Array,
    shownCards: Number,
    start: Boolean,
    activeCards: Array,
    itemClosed: Array,
  },
  beforeUpdate() {

  },
  methods: {
    clickOnCell() {
      if (this.start && this.shownCards < 2) {
        if (!this.itemClosed[this.$el.id]) {
          this.$el.innerHTML = this.items[this.$el.id];
          this.activeCards.push(this.$el.id);
          this.$emit('changeShownCards', this.shownCards + 1);
          // console.log(this.shownCards)
          console.log(this.activeCards)
        }
      }
    }
  }
}
</script>

<style scoped>
  .game-cell {
    width: 100px;
    height: 100px;
    border: 1px solid black;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
  }

  .completed {
    background: green;
  }
</style>
