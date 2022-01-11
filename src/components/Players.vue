<template>
  <div id="players">
    <h1>Enter players names :</h1>

    <input type="text" placeholder="Nom" v-model="player_name">
    <button @click="addPlayersName(player_name)" >Add</button>
    <ul>
      <li v-for="player in players" :key="player">{{ player }} <button @click="players.splice(players.indexOf(player), 1)" >delete</button></li>
    </ul>

    <button @click="readyToPlay()">Ready !</button>
  </div>
</template>

<script>

import {ref} from "vue";

class Player {

  constructor(name) {
    this.name = name;
    this.points = 0;
  }

}

export default {
  name: 'Players',
  data () {
    return {
      players: [],
    }
  },
  setup () {
    const player_name = ref("");
    return {
      player_name
    };
  },
  methods: {
    addPlayersName(player_name) {
      this.players.push(new Player(player_name));
      this.player_name = '';
    }
  }
}

</script>
