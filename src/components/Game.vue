<template>

  <Players/>
</template>

<script>
import Players from "./Players";
export default {

  components: {Players},
  props: [
      'players'
  ],
  name: "Game",
  methods: {
  }

}
</script>

<style scoped>

</style>
