<template>
  <div class="main-wrapper">
    <headerMenu />
    <blocksList />
  </div>
</template>

<script>
import blocksList from './components/blocks-list.vue';
import headerMenu from './components/header.vue';
export default {
  components: { headerMenu, blocksList },
};
</script>

<style lang="scss" scoped>
.main-wrapper {
  max-width: 450px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>
