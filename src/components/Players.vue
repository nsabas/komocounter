<template  v-if="isHidden">
  <div id="players">
    <h2>Enter players names :</h2>

    <div>
      <input v-on:keyup.enter="addPlayersName(player_name)" class="enter-plalyer-input" type="text" placeholder="Nom" v-model="player_name">
      <font-awesome-icon class="add-player-btn" @click="addPlayersName(player_name)" icon="plus" />
    </div>
    <ul>
      <li class="username-field" v-for="player in players" :key="player">{{ player.name }} <font-awesome-icon class="" @click="players.splice(players.indexOf(player), 1)" icon="times" /></li>
    </ul>

    <button class="btn" @click="readyToGame">Ready !</button>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import {ref} from "vue";
import { library } from '@fortawesome/fontawesome-svg-core'
import { faPlus, faTimes } from '@fortawesome/free-solid-svg-icons'

library.add(faPlus);
library.add(faTimes);
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
    this.isKomo = isKomo;
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
  components: {
    FontAwesomeIcon
  },
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
      if (player_name !== ''){
        this.players.push(new Player(player_name));
        this.player_name = '';
      }
    },
    readyToGame(){
      if (this.players.length > 0){
        this.$emit('start-game', this.players);
      }
    }
  }
}

</script>

<style>
#players {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.username-field {
  display: flex;
  align-items: center;
}

.enter-plalyer-input {
  border-radius: 20px;
  height: 25px;
}

.add-player-btn {
  margin-left: 10px;
}
</style>
