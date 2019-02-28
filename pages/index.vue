<template>
  <div class="h-screen text-grey-light pt-2 flex flex-col">
    <header class="container">
      <h1 class="logo mx-auto">Extreme Dares</h1>
    </header>

    <section class="container flex-1 pb-16" v-if="agreed">
      <div v-if="dares.length <= 0" class="block text-center my-16 max-w-sm mx-auto">
        <!-- Game over -->
        <p class="text-3xl">Completed it!</p>
        <p
          class="font-hairline text-xl my-10 leading-tight"
        >No more dare. If you made it this far give yourself a pat on the back.</p>
        <button @click="startAgain()">Start Again</button>
      </div>

      <!-- Dares -->
      <div v-else class="block text-center py-16 flex flex-col h-full">
        <p class="flex-1 text-2xl my-10 leading-tight">{{dares[selectedDare].dare}}</p>
        <div>
          <button @click.prevent="generateNewDare()">Roll the dice</button>
        </div>
      </div>
    </section>

    <section v-else class="container p-6">
      <p class="my-8 font-thin leading-tight">
        <span class="text-red-light">WARNING</span> Although these are made for fun, they are not for the faint hearted. Do them at your own risk. You have been warned.
      </p>
      <button @click="agreeToPlay()">Agree</button>
    </section>
  </div>
</template>

<script>
import data from '../assets/data'

let daresList = data

export default {
  data() {
    return {
      agreed: false,
      dares: daresList,
      selectedDare: Math.floor(Math.random() * daresList.length)
    }
  },
  methods: {
    generateNewDare() {
      this.dares.splice(this.selectedDare, 1)
      this.selectedDare = this.randomNumber()
    },
    randomNumber() {
      return Math.floor(Math.random() * this.dares.length)
    },
    agreeToPlay() {
      // Set local storage
      localStorage.setItem('agree', true)
      this.agreed = true
    },
    startAgain() {
      this.$router.go()
    }
  },
  created() {
    if (process.browser) {
      // Check if the user has already agreed to play
      if (localStorage.getItem('agree')) {
        this.agreed = true
      }
    }
  }
}
</script>

 <style>
.text-gradient {
  background: linear-gradient(to right, #d9a185 -100%, #d2506f 100%);
  background-clip: text;
  display: inline-block;
  color: transparent;
}
.logo {
  background: url('~assets/images/logo.png') no-repeat center center;
  background-size: contain;
  width: 250px;
  height: 160px;
  display: block;
  text-indent: -99999px;
}
button {
  background: #cecece;
  border-radius: 999px;
  padding: 0.75rem 1.25rem;
  display: inline-block;
  font-weight: bold;
  cursor: pointer;
  font-size: 1.125rem;
  box-shadow: 0 15px 30px 0 rgba(0, 0, 0, 0.11), 0 5px 15px 0 rgba(0, 0, 0, 0.08);
}
</style>
