<template>

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

  <GridPoint :players="game.players"/>
</template>

<script>
import Players from "./Players";
import Cards from "./Cards";
import Komo from "./Komo";
import GridPoint from "./GridPoint";

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
    GridPoint
  },
  data() {
    return {
      game: Game,
      currentRound: 1,
      isHiddenEnterPlayerStep: false,
      isHiddenStartGameStep: true,
      isHiddenEndGame: true,
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
    }
  }

}
</script>

<style scoped>

</style>
