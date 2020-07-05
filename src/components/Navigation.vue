<template>
  <div>
    <v-app-bar app color="primary">
      <v-toolbar-title class="headline text-uppercase">
        <span>
          <router-link to="/" tag="span" style="cursor: pointer">
            <i class="fas fa-paw" style="color: #444; font-size: 54px;"></i>
            <span style="font-size: 30px; margin-left: 10px; color: #fff;">Hills Promotion</span>
          </router-link>
        </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn elevation="0" color="#B71C1C" style="color: #fff;">
        <span class="mr-2">
          <router-link to="/entrants" tag="span">Entrants</router-link>
        </span>
      </v-btn>
    </v-app-bar>
  </div>
</template>