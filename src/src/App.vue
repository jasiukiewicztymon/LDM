
<template>
  <MenuElement/>
  <ModelisationArea/>
  <GithubPointer/>
</template>

<script>
import MenuElement from './components/MenuElement.vue'
import ModelisationArea from './components/ModelisationArea.vue'
import GithubPointer from './components/GithubPointer.vue'
export default {
  name: 'App',
  components: {
    MenuElement,
    ModelisationArea,
    GithubPointer
  },
  data() {
    return {
    }
  },
  methods: {
  }
}
</script>
