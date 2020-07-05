<template>
  <div>
    <v-card elevation="8" width="300" height="300">
      <v-card-title class="title" style="font-size: 48px;">{{ client.name }}</v-card-title>
      <span class="bold">Phone Number:</span>
      <v-card-text>{{ client.phone }}</v-card-text>
      <span class="bold">Product:</span>
      <v-card-text>{{ client.description }} {{ client.size }}</v-card-text>
      <span class="bold">POS Number:</span>
      <v-card-text>{{ client.posNumber }}</v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    client: Object
  }
};
</script>

<style scoped>
* {
  padding: 0 5px 10px 10px;
}

.title {
  margin-bottom: 20px;
  font-size: 2rem;
  padding-top: 20px;
}

.bold {
  font-weight: bold;
}
</style>