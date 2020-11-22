<template>
  <div id="app">
      <AppPageForm/>
  </div>
</template>

<script>
import AppPageForm from "./pages/form"
export default {
  name: 'App',
  components: {
      AppPageForm
  }
}
</script>

<style lang="scss">
    @import "styles/index.scss";
</style>
