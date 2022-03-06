<template>
  <MenuElement/>
  <ModelisationArea>
    <slot name="table">
      <input type="text">
      <button>Add Value</button>
    </slot>
  </ModelisationArea>
  <GithubPointer/>
</template>

<script>
import MenuElement from './components/MenuElement.vue'
import GithubPointer from './components/GithubPointer.vue'
import ModelisationArea from './components/ModelisationArea.vue'

export default {
  name: 'App',
  components: {
    MenuElement,
    GithubPointer,
    ModelisationArea,
  },
  data() {
    return {
    }
  },
  methods: {

  }
}
</script>
  
<style lang="sass" scoped>
</style>
