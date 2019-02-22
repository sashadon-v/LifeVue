<template>
  <div id='app'>
    <Field :width='width' :height='height' :cells='cells' />
    <input type="number" v-model="width">
    <input type="number" v-model="height">
    <button @click="build">build</button>
    <button @click="start">start</button>
    <input v-model="gameId">
    <button @click="move">move</button>
    <button @click="simulate">simulate</button>
  </div>
</template>

<script>
import axios from 'axios'
import Field from './components/Field'

export default {
  name: 'app',
  components: {
    Field
  },
  data () {
    return {
      gameId: null,
      simulateId: null,
      width: 10,
      height: 10,
      cells: []
    }
  },
  created () {
    this.build()
  },
  methods: {
    build () {
      this.cells = []
      for (let y = 0; y < this.height; y++) {
        for (let x = 0; x < this.width; x++) {
          this.cells.push({
            x,
            y,
            value: false
          })
        }
      }
    },
    start () {
      console.log('start')
      axios.post(`http://localhost:8082/game/start?w=${this.width}&h=${this.height}`, this.cells).then(response => {
        this.gameId = response.data
      })
    },
    move () {
      console.log('move')
      axios.post(`http://localhost:8082/game/move?id=${this.gameId}`).then(response => {
        this.cells = response.data
      }).catch((error) => {
        clearInterval(this.simulateId)
      })
    },
    simulate () {
      this.simulateId = setInterval(() => {
        this.move()
      }, 200)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
}
</style>
