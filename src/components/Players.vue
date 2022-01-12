<template v-if="isHidden">
  <div>
    <h1>Enter players names :</h1>

    <input type="text" placeholder="Nom" v-model="player_name">
    <button @click="addPlayersName(player_name)" >Add</button>
    <ul>
      <li v-for="player in players" :key="player">{{ player.name }} <button @click="players.splice(players.indexOf(player), 1)" >delete</button></li>
    </ul>

    <button @click="readyToGame">Ready !</button>
  </div>
</template>

<script>

import {ref} from "vue";

export class Player {
  constructor(name) {
    this.name = name;
    this.points = 0;
    this.isKomo = false;
  }

  addPoints(points){
    if ((this.points + points) % 50 === 0){
      this.points = 0;
    } else {
      this.points += points;
    }
  }

  setKomo(isKomo){
    this.komo = isKomo;
  }

  getPoints(){
    return this.points;
  }

  winKomo(){
    this.addPoints(-10);
  }

  looseKomo(){
    this.addPoints(20);
  }
}

export default {
  name: 'Players',
  props: {
    isHidden: Boolean
  },
  data () {
    return {
      players: []
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
    },
    readyToGame(){
      if (this.players.length > 0){
        this.$emit('start-game', this.players);
      }
    }
  }
}

</script>
