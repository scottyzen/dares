<template>
  <div class="container h-screen text-grey-light pt-2 flex flex-col">
    <header>
      <h1 class="mt-4 text-gradient text-5xl logo mx-auto">Extreme Dares</h1>
    </header>

    <section class="flex-1">
      <div
        v-if="dares.length <= 0"
      >No more dare. If you made it this far give yourself a pat on the back.</div>
      <div v-else class="block text-center my-16">
        <!-- Dare -->
        <p
          class="max-w-sm font-hairline text-2xl mx-auto mt-6 mb-16 leading-tight"
        >{{dares[selectedDare].dare}}</p>

        <!-- Roll the dice -->
        <a
          class="inline-block rounded py-3 px-4 cursor-pointer border border-grey shadow-lg"
          @click="generateNewDare()"
        >Roll the dice</a>
      </div>
    </section>

    <footer>
      <p class="my-4 text-sm font-thin leading-tight">
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
  background: url('~assets/images/logo.png') no-repeat;
  background-size: contain;
  width: 300px;
  height: 180px;
  display: block;
}
</style>
