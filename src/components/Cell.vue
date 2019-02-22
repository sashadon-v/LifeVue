<template>
  <div @click="clickHandler" :class="{ 'cell': true, 'cell--active': value }" :style="{top: y*20 + 'px', left: x*20 + 'px'}"></div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    x: Number,
    y: Number,
    value: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
    }
  },
  methods: {
    clickHandler () {
      console.log('cell emit -> ', !this.value)
      this.$emit('value', !this.value)
    }
  }
}
</script>
<style scoped>
  .cell {
    border: 1px solid #ccc;
    position: absolute;
    width: 20px;
    height: 20px;
  }
  .cell--active {
    background-color: black;
  }
</style>
