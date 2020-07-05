<template>
  <v-app>
    <navigation></navigation>
    <router-view />
  </v-app>
</template>

<script>
import Navigation from "./components/Navigation.vue";

export default {
  name: "App",
  components: {
    Navigation
  }
};
</script>

<style>
* {
  font-family: "Rubik";
}
</style>
