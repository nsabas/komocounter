<template>
  <div>
    <div v-if="players.length > 0">

      <row :gutter="50" :columns="3">
        <column :xs="12" :lg="4">
<!--          left arrow    -->
          <font-awesome-icon @click="prevPlayer" icon="angle-left" />
        </column>
        <column :xs="12" :lg="4">
          <img id="avatar" :src="avatarUrl + players[currentIndex].name + '.svg'">
          <h2>{{ players[currentIndex].name }}</h2>
          <div v-if="!players[currentIndex].isKomo">
            <input type="number" v-model="currentPoints">
            <button @click="addPointsToPlayer(currentPoints)">Add points</button>
          </div>
          <div v-if="players[currentIndex].isKomo">
            <h4>So how was this komo ?</h4>
            <div class="grid-container">

              <div class="grid-child purple">
                <button class="btn komo-btn-win" @click="komoWin">Win</button>
              </div>

              <div class="grid-child green">
                <button class="btn komo-btn-fail" @click="komoLoose">Loose</button>
              </div>

            </div>
          </div>
        </column>
        <column :xs="12" :lg="4">
<!--          right arrow   -->
          <font-awesome-icon @click="nextPlayer" icon="angle-right" />
        </column>
      </row>
    </div>

  </div>
</template>

<script>
import {Row, Column} from 'vue-grid-responsive';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faAngleRight, faAngleLeft } from '@fortawesome/free-solid-svg-icons';


library.add(faAngleRight);
library.add(faAngleLeft);
export default {
  name: "Cards",
  components: {
    Row,
    Column,
    FontAwesomeIcon
  },
  props: {
    players: Array
  },
  data() {
    return {
      currentIndex: 0,
      currentPoints: 0,
      avatarUrl: 'https://avatars.dicebear.com/api/avataaars/'
    }
  },
  methods: {
    nextPlayer() {
      if (this.currentIndex + 1 < this.players.length) {
        this.currentIndex += 1;
      } else {
        this.currentIndex = 0;
        this.currentPoints = 0;
        this.$emit('round-finished');
      }
    },
    prevPlayer() {
      if (this.currentIndex - 1 >= 0) {
        this.currentIndex -= 1;
      }
    },
    addPointsToPlayer(points) {
      this.players[this.currentIndex].addPoints(points);
      this.currentPoints = 0;
      this.nextPlayer();
    },
    komoWin() {
      this.players[this.currentIndex].winKomo();
      this.players[this.currentIndex].setKomo(false);
      this.nextPlayer();
    },
    komoLoose() {
      this.players[this.currentIndex].looseKomo();
      this.players[this.currentIndex].setKomo(false);
      this.nextPlayer();
    }
  }
}
</script>

<style>
.grid-row {
  flex-wrap: nowrap;
}
/*// Basic Button Style*/
.btn {
  box-sizing: border-box;
  appearance: none;
  background-color: transparent;
  border: 0;
  border-radius: 0.6em;
  color: black;
  cursor: pointer;
  display: flex;
  align-self: center;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1;
  padding: 1.2em 2.8em;
  text-decoration: none;
  text-align: center;
  font-family: 'Montserrat', sans-serif;
}

.komo-btn-fail {
  background-color: #EA3546;
}

.komo-btn-win {
  background-color: #F9C80E;
}
.grid-container {
  display: flex;
  flex-direction: row;

}

#avatar {
  width: 200px;
  height: 150px;
}
</style>
