<script>
import AppHeader from './components/AppHeader.vue';

export default{
  components: {
    AppHeader
  }

}
</script>

<template>
  <AppHeader></AppHeader>
  <router-view> </router-view>
</template>

<style lang="scss">
@use './style/generic';
@use './style/partials/variables' as *;

</style>
