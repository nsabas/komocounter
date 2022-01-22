<template>
  <div>
    <h2>Who's Komo ?</h2>
    <div class="container">
      <div  class="slot" v-for="(player, index) in players" :key="player" @click="hasKomo(index)">
        <button>{{ player.name }}</button>
      </div>
    </div>
    <button class="btn" @click="hasKomo(undefined)">skip</button>
  </div>
</template>

<script>
export default {
  name: "Komo",
  props: {
    players: Array
  },
  methods: {
    hasKomo(index){
      if (index !== undefined){
        this.players[index].setKomo(true);
      }
      this.nextStep();
    },
    nextStep(){
      this.$emit('komo-choosen');
    }
  }
}
</script>

<style scoped>

.container {
  display: flex;
  flex-wrap: wrap;
}
.slot {
  flex: 1 1 50%;
  margin-top: 30px;
}

.slot > * {
  box-sizing: border-box;
  appearance: none;
  border: 0;
  background-color: transparent;
  font-family: 'Montserrat', sans-serif;
  font-size: 1.5rem;
}

</style>
