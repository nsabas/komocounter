<template>
<div>
  <h2>Grid Points</h2>
  <table>
    <tr>
      <td v-for="player in players" :key="player">{{ player.name }}</td>
    </tr>
    <tr>
      <td v-for="player in players" :key="player">{{ player.points }}</td>
    </tr>
  </table>
</div>
</template>

<script>
export default {
  name: "GridPoint",
  props: {
    players: Array
  }
}
</script>

<style scoped>

</style>
