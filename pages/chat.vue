<template>
  <h1>Chat Page {{ user.name }}</h1>

</template>

<script>
  import {mapState} from 'vuex';
  export default {
    name: "chat",
    middleware: ['chat'],
    computed: mapState(["user"]),
  }
</script>

<style scoped>

</style>
