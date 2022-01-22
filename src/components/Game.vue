<template>
  <div @click="showGridPoints" v-if="isHiddenGridPoints && isHiddenEnterPlayerStep" class="grid-points">
    <font-awesome-icon icon="coins" /><div>points</div>
  </div>
  <div @click="hideGridPoints" v-if="!isHiddenGridPoints && isHiddenEnterPlayerStep" class="grid-points">
    <font-awesome-icon icon="times" />
  </div>

  <!-- get players names -->
  <Players v-if="!isHiddenEnterPlayerStep" @start-game="getPlayersList"/>
  <!-- end -->

  <!-- ask if someone has komo -->
  <Komo v-if="!isHiddenAskKomoStep && game.players" :players="game.players" @komo-choosen="countPoint" />
  <!-- end -->

  <!-- enter points for each player -->
  <Cards v-if="!isHiddenStartGameStep && game.players" :players="game.players" @round-finished="nextRound"/>
  <!-- end -->

  <!-- points grid -->
  <div v-if="!isHiddenEndGame">
    <h1>End Game</h1>
    <div>well done !</div>
  </div>
  <!-- end -->


  <GridPoint v-if="!isHiddenGridPoints" :players="game.players"/>
</template>

<script>
import Players from "./Players";
import Cards from "./Cards";
import Komo from "./Komo";
import GridPoint from "./GridPoint";
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faCoins, faTimes } from '@fortawesome/free-solid-svg-icons'

library.add(faCoins);
library.add(faTimes);
export class Game {
  players;
  constructor(playersList = [], nbRound = 5) {
    this.players = playersList;
    this.nbRound = nbRound
  }

  getNbRound(){
    return this.nbRound;
  }

  getplayers(){
    return this.players
  }
}

export default {
  components: {
    Players,
    Cards,
    Komo,
    FontAwesomeIcon,
    GridPoint
  },
  data() {
    return {
      game: Game,
      currentRound: 1,
      isHiddenEnterPlayerStep: false,
      isHiddenStartGameStep: true,
      isHiddenEndGame: true,
      isHiddenGridPoints: true,
      isHiddenAskKomoStep: true
    }
  },
  name: "Game",
  methods: {
    getPlayersList(players){
      this.game = new Game(players);
      this.isHiddenEnterPlayerStep = true
      this.isHiddenAskKomoStep = false
    },
    countPoint(){
      this.isHiddenAskKomoStep = true;
      this.isHiddenStartGameStep = false;
    },
    nextRound(){
      if (this.currentRound + 1 <= this.game.getNbRound()){
        this.currentRound += 1;
        this.isHiddenStartGameStep = true;
        this.isHiddenAskKomoStep = false
      } else {
        this.isHiddenStartGameStep = true;
        this.isHiddenEndGame = false;
      }
    },
    showGridPoints(){
      this.isHiddenStartGameStep = true;
      this.isHiddenAskKomoStep = true;
      this.isHiddenEndGame = true;
      this.isHiddenGridPoints = false;
    },
    hideGridPoints(){
      this.isHiddenStartGameStep = false;
      this.isHiddenGridPoints = true;
    }
  }

}
</script>

<style scoped>
.grid-points {
  position: absolute;
  bottom: 0px;
  right: 0px;
}

</style>
