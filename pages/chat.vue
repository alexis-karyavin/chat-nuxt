<template>
  <h1>Chat Page {{ user.name }}</h1>

</template>

<script>
  import {mapState} from 'vuex';
  export default {
    name: "chat",
    middleware: ['chat'],
    head() {
      return {
        title: 'Комната ' + this.user.room
      }
    },
    computed: mapState(["user"]),
  }
</script>

<style scoped>

</style>
