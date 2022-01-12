<template>
  <div>
    <h1>Who's Komo ?</h1>
    <button v-for="(player, index) in players" :key="player" @click="hasKomo(index)">{{ player.name }}</button>
    <button @click="hasKomo(undefined)">skip</button>
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

</style>
