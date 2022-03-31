<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6" md="3"> </v-col>
      <v-form>
        <v-text-field label="Regular" v-model="ime"></v-text-field>
        <v-btn @click="getData"> Submit </v-btn>
        <v-data-table
          :headers="headers"
          :items="items"
          :items-per-page="9"
          class="elevation-1"
        ></v-data-table>
      </v-form>
    </v-row>
  </v-container>
</template>

<script>
/* eslint-disable */

export default {
  ime: 'HomeView',
  data: function() {
    return {
      ime: "",
      items: [],
      headers: [
        {
          text: "Ime",
          align: "start",
          sortable: false,
          value: "ime",
        },
        {
          text: "Vjerojatnost",
          align: "start",
          sortable: false,
          value: "vjerojatnost",
        },
        {
          text: "Godine",
          align: "start",
          sortable: true,
          value: "godine",
        },
        {
          text: "Spol",
          align: "start",
          sortable: false,
          value: "spol",
        },
      ],

    };
  },
  methods: {
    async getData() {
      let podatci = await fetch("https://api.agify.io?name=" + this.ime);
      let podatci2 = await fetch("https://api.genderize.io?name=" + this.ime);
      let podatci3 = await fetch(
        "https://api.nationalize.io?name=" + this.ime
      );

      let rezultati = await podatci.json();
      let rezultati2 = await podatci2.json();
      let rezultati3 = await podatci3.json();

      let temp = {
        ime: rezultati.ime,
        godine: rezultati.age,
        spol: rezultati.gender,
        vjerojatnost: rezultati.probability,
      };
      this.items.push(temp);

      console.log(rezultati);
      console.log(rezultati2);
      console.log(rezultati3);
    },
  },
};
</script>
