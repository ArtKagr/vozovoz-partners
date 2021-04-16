<template>
  <div class="d-flex flex-column vh-100 vw-100 overflow-auto">
    <Header class="w-100 align-self-start" />
    <Nuxt class="align-self-stretch w-100 h-100 overflow-auto" />
  </div>
</template>
<script>
import Header from '../components/header'
export default {
  components: { Header },
}
</script>
<style lang="scss">
@import '../assets/scss/app.scss';
</style>
