<template>
  <div class="field">
    <Cell v-for="cell in cells" :x="cell.x" :y="cell.y" :value="cell.value" :key="'asd' + cell.x + '' + cell.y" @value="valueHandler(cell, $event)" />
  </div>
</template>

<script>
import Cell from './Cell'

export default {
  name: 'Field',
  components: {
    Cell
  },
  props: {
    width: Number,
    height: Number,
    cells: Array
  },
  data () {
    return {
    }
  },
  methods: {
    valueHandler (cell, value) {
      cell.value = value
    }
  }
}
</script>
<style scoped>
  .field {
    width: 100%;
    height: 100%;
  }
</style>
