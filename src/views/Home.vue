<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <h1
              style="text-align: center; font-weight: 400;"
            >Buy 1 Bag of Hills pet food & go into the draw to win a free bag.</h1>
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Login form</v-toolbar-title>
                <div class="flex-grow-1"></div>
              </v-toolbar>
              <v-card-text>
                <v-form ref="form">
                  <v-text-field
                    label="Name"
                    name="name"
                    prepend-icon="person"
                    type="text"
                    v-model="name"
                    required
                  ></v-text-field>
                  <v-text-field
                    id="phone"
                    label="Number"
                    name="phone"
                    prepend-icon="phonelink_ring"
                    type="number"
                    v-model="number"
                    required
                  ></v-text-field>
                  <v-select
                    :items="products"
                    label="Description"
                    prepend-icon="description"
                    v-model="description"
                    required
                  ></v-select>
                  <v-text-field
                    id="size"
                    label="Size (Kg)"
                    name="size"
                    prepend-icon="pets"
                    type="text"
                    v-model="size"
                    required
                  ></v-text-field>
                  <v-text-field
                    id="pos"
                    label="POS NO."
                    name="pos"
                    prepend-icon="attach_money"
                    type="text"
                    v-model="posNumber"
                    required
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <div class="flex-grow-1"></div>
                <v-btn
                  color="primary"
                  @click="addClient"
                  @keyup.enter="addClient"
                  :disabled="!formIsValid"
                >Enter</v-btn>
              </v-card-actions>
            </v-card>
            <v-snackbar v-model="snackbar" :timeout="timeout" color="success">
              {{ text }}
              <v-icon style="color: #fff;">tag_faces</v-icon>
            </v-snackbar>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
//import products from "../products.js";
//import firebase from "firebase";

/* const config = {
  apiKey: "AIzaSyCE4PkKWCdcQCaOLoN3aEpTyNJdvG7souM",
  authDomain: "hills-promo.firebaseapp.com",
  databaseURL: "https://hills-promo.firebaseio.com",
  projectId: "hills-promo",
  storageBucket: "hills-promo.appspot.com",
  messagingSenderId: "471002326563",
  appId: "1:471002326563:web:a7ac1374fc1bcadd9b3396",
  measurementId: "G-LPL3BFTFQ8"
};

let app = firebase.initializeApp(config);
let db = app.database();

let clientsRef = db.ref("clients"); */
import axios from "axios";
export default {
  data() {
    return {
      name: "",
      number: "",
      description: "",
      size: "",
      posNumber: "",

      snackbar: false,
      text: "You are in the draw. Good Luck!",
      timeout: 3000,
      /*
      clients: [
        { name: "", number: "", description: "", size: "", posNumber: "" }
      ],
      */

      products: [
        "Hills Feline Oral Care ",
        "Hills Feline Adult Hairball Control",
        "Hills Feline Kitten",
        "Hills Feline Sensitive Skin & Stomach",
        "Hills Feline Light",
        "Hills Feline Senior Hairball Control (7+)",
        "Hills Feline Adult 7+",
        "Hills Feline Youthful Vitality",
        "Hills Feline Adult 1-6",
        "Hills Canine Adult Large Breed Light",
        "Hills Canine Adult 1-6",
        "Hills Canine Puppy Large Breed",
        "Hills Canine Puppy Small Bites",
        "Hills Canine Adult Light",
        "Hills Canine Youthful Vitality",
        "Hills Canine Adult 7+ Small Bites",
        "Hills Canine Adult Large Breed",
        "Hills Canine Adult 1-6 Small bites",
        "Hills Canine Adult Sensitive Stomach & Skin",
        "Hills Canine Adult Large Breed 6+",
        "Hills Canine Adult 7+"
      ]
    };
  },
  computed: {
    formIsValid() {
      return (
        this.name !== "" &&
        this.number !== "" &&
        this.description !== "" &&
        this.size !== "" &&
        this.posNumber !== ""
      );
    }
  },
  methods: {
    addClient() {
      var data = {
        name: this.name,
        phone: this.number,
        description: this.description,
        size: this.size,
        posNumber: this.posNumber
      };

      axios
        .post("https://hills-promotion-a6c80.firebaseio.com/clients.json", data)
        .then(response => {
          console.log(response);
        });

      this.snackbar = true;

      this.name = "";
      this.number = "";
      this.description = "";
      this.size = "";
      this.posNumber = "";
    }
  }
};
</script>

<style scoped>
h1 {
  text-align: center;
  font-size: 35px;
}
</style>
