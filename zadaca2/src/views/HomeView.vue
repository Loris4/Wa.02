<template>
  <v-container>
    <v-row>
      <v-col cols="13" sm="5" md="3"> </v-col>
      <v-form>
        <v-text-field label="Regular" v-model="ime"></v-text-field>
        <v-btn @click="getData"> Submit </v-btn>
        <v-data-table
          :headers="headers"
          :items="items"
          :items-per-page="5"
          class="elevation-5"
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
          text: "IME",
          align: "middle",
          sortable: true,
          value: "ime",
        },
        {
          text: "VJEROJATNOST",
          align: "start",
          sortable: true,
          value: "vjerojatnost",
        },
        {
          text: "GODINE",
          align: "middle",
          sortable: true,
          value: "godine",
        },
        {
          text: "SPOL",
          align: "start",
          sortable: true,
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
        ime: rezultati.name,
        godine: rezultati.age,
        spol: rezultati2.gender,
        vjerojatnost: rezultati2.probability,
      };
      this.items.push(temp);

      console.log(rezultati);
      console.log(rezultati2);
      console.log(rezultati3);
    },
  },
};
</script>
