<template>
  <div class="h-screen text-grey-light pt-2 flex flex-col">
    <header class="container">
      <h1 class="logo mx-auto">Extreme Dares</h1>
    </header>

    <section class="container flex-1">
      <div v-if="dares.length <= 0" class="block text-center my-16">
        <p
          class="max-w-sm font-hairline text-2xl mx-auto my-10 leading-tight"
        >No more dare. If you made it this far give yourself a pat on the back.</p>
      </div>
      <div v-else class="block text-center my-16">
        <!-- Dare -->
        <p
          class="max-w-sm font-hairline text-2xl mx-auto my-10 leading-tight"
        >{{dares[selectedDare].dare}}</p>

        <!-- Roll the dice -->
        <button
          class="inline-block py-3 px-5 cursor-pointer font-bold shadow-lg rounded-full"
          @click="generateNewDare()"
        >Roll the dice</button>
      </div>
    </section>

    <footer>
      <p class="p-4 text-sm font-thin leading-tight">
        <span class="text-red-light">WARNING</span> Although these are made for fun, they are not for the faint hearted. Do them at your own risk. You have been warned.
      </p>
    </footer>
  </div>
</template>

<script>
import data from '../assets/data'

var daresList = data

export default {
  head: {
    title: 'Welcome',
    meta: [{ hid: 'description', name: 'description', content: 'Welcome' }]
  },
  data() {
    return {
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
  /* border: 1px solid rgb(46, 46, 46); */
}
</style>
