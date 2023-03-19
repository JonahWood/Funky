<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-12 d-flex justify-content-center">
        <button class="btn btn-dark text-light" @click="playSound('background.mp3')">music</button>
        <button class="btn btn-dark text-light" @click="tempReset()">tempory reset</button>
        <button class="btn btn-primary" @click="getMana()">Get Mana</button>
      </div>
    </div>
  </div>
<div class="container-fluid background-text py-3 mt-5 bg-gradient">
  <div class="row">
    <div class="col-3">
      <h1 class="text-light">HP: <span :class="playerHealth == 0 ? 'text-danger' : ''">{{ playerHealth }}</span></h1>

      <!-- mana vvv -->
      <h1 class="text-primary d-flex align-content-center">
        <img class="mana-img" src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/a09197d9-eba7-4153-9b04-b7d0002e2633/ddkkg2f-e3ba0c61-fc04-45b7-bce0-6d319f8036b9.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcL2EwOTE5N2Q5LWViYTctNDE1My05YjA0LWI3ZDAwMDJlMjYzM1wvZGRra2cyZi1lM2JhMGM2MS1mYzA0LTQ1YjctYmNlMC02ZDMxOWY4MDM2YjkuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.BFRuHCYSxaPRhRGJKHxvlsoc2iZ3CGZIvn4BO6vpx6s" alt="">: {{ mana }}
      </h1>

      <img class="player-monkey img-fluid" src="monke-face-right.gif" alt="">
    </div>
    <div class="col-3 offset-6">
      <h1 class="text-light">HP: <span :class="opponentHealth == 0 ? 'text-success' : ''">{{ opponentHealth }}</span></h1>
      <img src="monke-face-left.gif" alt="">
    </div>
    <div class="col-12 d-flex justify-content-around text-light">
      <div><button @click="attackOne()" class="btn btn-warning">Slap</button><h3>Cost: <span class="text-primary">15</span></h3></div>
      <div><button @click="attackTwo()" class="btn btn-warning">Punch</button><h3>Cost: <span class="text-primary">30</span></h3></div>
      <div><button @click="attackThree()" class="btn btn-warning">Slam</button><h3>Cost: <span class="text-primary">45</span></h3></div>
      <div><button @click="attackFour()" class="btn btn-warning">Grab 'n' throw</button><h3>Cost: <span class="text-primary">80</span></h3></div>
    </div>
  </div>
  
</div>
</template>

<script>
import { watchEffect, computed, onMounted } from 'vue';
import { logger } from '../utils/Logger';
import { AppState } from '../AppState.js';
import Pop from '../utils/Pop';


export default {
  setup() {
let musicCheck = true
    return {
      playerHealth: computed(()=> AppState.playerHealth),
      opponentHealth: computed(()=> AppState.opponentHealth),
      mana: computed(()=> AppState.mana),
      musicCheck, 
      attackOne(){
        if (AppState.opponentHealth-10 <= 0) {
          AppState.opponentHealth = 0
          Pop.success('Enemy Defeated!')
        } else {
          AppState.opponentHealth -= 10 
          if (AppState.mana >= 15) {
            AppState.mana -= 15
          } else {
            Pop.error('You do not have enough mana!')
          }
        }
        logger.log('attack one - ', 'player health:', this.playerHealth, 'opponent health:', this.opponentHealth)
      },
      attackTwo(){
        if (AppState.opponentHealth-20 <= 0) {
          AppState.opponentHealth = 0
          Pop.success('Enemy Defeated!')
        } else {
          AppState.opponentHealth -= 20
          if (AppState.mana >= 30) {
            AppState.mana -= 30
          } else {
            Pop.error('You do not have enough mana!')
          }
        }
        logger.log('attack two - ', 'player health:', this.playerHealth, 'opponent health:', this.opponentHealth)
      },
      attackThree(){
        if (AppState.opponentHealth-30 <= 0) {
          AppState.opponentHealth = 0
          Pop.success('Enemy Defeated!')
        } else {
          AppState.opponentHealth -= 30
          if (AppState.mana >= 45) {
            AppState.mana -= 45
          } else {
            Pop.error('You do not have enough mana!')
          }
        }
        logger.log('attack three - ', 'player health:', this.playerHealth, 'opponent health:', this.opponentHealth)
      },
      attackFour(){
        if (AppState.opponentHealth-40 <= 0) {
          AppState.opponentHealth = 0
          Pop.success('Enemy Defeated!')
        } else {
          AppState.opponentHealth -= 40
          if (AppState.mana >= 80) {
            AppState.mana -= 80
          } else {
            Pop.error('You do not have enough mana!')
          }
        }
        logger.log('attack four - ', 'player health:', this.playerHealth, 'opponent health:', this.opponentHealth)
      },
      tempReset(){
        AppState.opponentHealth = 100
        AppState.playerHealth = 100
        AppState.mana = 100
      },
      playSound(sound){
if (musicCheck) {
  let audio = new Audio(sound);
        audio.play();
        audio.volume = 0.1
        audio.loop = true
        musicCheck = false
        Pop.success('Music Initialized!')
} else {
  Pop.toast('Audio already playing!')
}
}, 
getMana(){
  // let manaGet = 
// AppState.mana += Math.round(Math.random*10)
AppState.mana += 1
},
    }
  }
}
</script>

<style scoped lang="scss">
.mana-img{
  height: 10vh;
}

.background-text{
  background-color: rgba(65, 36, 11, 0.662);
}

.home {
  display: grid;
  height: 80vh;
  place-content: center;
  text-align: center;
  user-select: none;

img{
  height: 100vh;
  width: 100%;
}
}
</style>
