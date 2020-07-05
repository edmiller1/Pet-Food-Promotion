<template>
  <div>
    <v-container class="container">
      <v-row v-if="otherCondition" class="mx-auto row">
        <v-btn disabled class="mx-auto" color="primary" @click="selectWinner">Generate A Winner</v-btn>
        <v-row style="width: 100%;" class="mx-auto">
          <h1 class="mx-auto">Zero Entries</h1>
        </v-row>
      </v-row>
      <v-row v-else-if="firstCondition">
        <v-row style="width: 100%;" class="mx-auto">
          <h1 class="mx-auto">Picking A Winner...</h1>
        </v-row>
        <v-row>
          <v-progress-circular style="width: 100px;" class="mx-auto" indeterminate color="primary"></v-progress-circular>
        </v-row>
      </v-row>
      <v-row class="mx-auto" v-else-if="secondCondition">
        <v-row style="width: 100%; text-align: center; margin-left: 30%;">
          <h1 style="font-size: 54px;">Congratulations!!</h1>
        </v-row>
        <v-row style="margin-left: 37%;">
          <client-cards :key="rnd.id" v-for="rnd in rndArray" :client="rnd"></client-cards>
        </v-row>
      </v-row>
      <v-row v-else-if="thirdCondition" class="mx-auto">
        <v-row class="mx-auto">
          <v-btn class="mx-auto" color="primary" @click="selectWinner">Generate A Winner</v-btn>
          <h1>Entries: &nbsp;</h1>
          <h1>{{ clients.length }}</h1>
        </v-row>
        <v-row class="mx-auto">
          <client-cards :key="client.id" v-for="client in clients" :client="client"></client-cards>
        </v-row>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";
import ClientCards from "../components/ClientCards.vue";

export default {
  data() {
    return {
      clients: [],
      rndArray: [],
      isRandom: false,
      isLoading: false
    };
  },
  methods: {
    selectWinner() {
      this.rndArray.push(
        this.clients[Math.floor(Math.random() * this.clients.length)]
      );
      setTimeout(() => {
        this.isLoading = false;
      }, 3000);
      this.isLoading = true;
      this.isRandom = true;
    }
  },
  computed: {
    firstCondition() {
      return this.isLoading == true;
    },
    secondCondition() {
      return this.isLoading == false && this.isRandom == true;
    },
    thirdCondition() {
      return this.isRandom == false && this.isLoading == false;
    },
    otherCondition() {
      return this.clients.length === 0;
    },
    someOtherCondition() {
      return this.clients.length > 0;
    },
    length() {
      return this.clients.length;
    }
  },
  created() {
    axios
      .get("https://hills-promotion-a6c80.firebaseio.com/clients.json")
      .then(response => {
        const obj = response.data;
        for (let key in obj) {
          this.clients.push({
            id: key,
            name: obj[key].name,
            phone: obj[key].phone,
            description: obj[key].description,
            size: obj[key].size,
            posNumber: obj[key].posNumber
          });
        }
        return this.clients;
      })
      .catch(error => {
        console.log(error);
      });
  },
  components: {
    ClientCards
  }
};
</script>

<style scoped>
.container {
  margin-top: 100px;
}

.row {
  margin-bottom: 30px;
}
</style>