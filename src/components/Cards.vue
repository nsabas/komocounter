<template>
<div>
  <div v-if="players.length > 0">
    <h2>{{ players[currentIndex].name }}</h2>
    <div v-if="!players[currentIndex].komo">
      <input type="number" v-model="currentPoints">
      <button @click="addPointsToPlayer(currentPoints)">Add points</button>
    </div>
    <div v-if="players[currentIndex].komo">
      <h4>So how was this komo ?</h4>
      <button @click="komoWin">Win</button>
      <button @click="komoLoose">Loose</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Cards",
  props: {
    players: Array
  },
  data(){
    return {
      currentIndex: 0,
      currentPoints: 0
    }
  },
  methods: {
    nextPlayer(){
      if (this.currentIndex + 1 < this.players.length){
        this.currentIndex += 1;
      } else {
        this.currentIndex = 0;
        this.currentPoints = 0;
        this.$emit('round-finished');
      }
    },
    prevPlayer(){
      if (this.currentIndex - 1 >= 0){
        this.currentIndex -= 1;
      }
    },
    addPointsToPlayer(points){
      this.players[this.currentIndex].addPoints(points);
      this.currentPoints = 0;
      this.nextPlayer();
    },
    komoWin(){
      this.players[this.currentIndex].winKomo();
      this.players[this.currentIndex].setKomo(false);
      this.nextPlayer();
    },
    komoLoose(){
      this.players[this.currentIndex].looseKomo();
      this.players[this.currentIndex].setKomo(false);
      this.nextPlayer();
    }
  }
}
</script>

<style scoped>

</style>
