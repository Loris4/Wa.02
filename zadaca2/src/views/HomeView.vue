<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6" md="3"> </v-col>
      <v-form>
        <v-text-field label="Regular" v-model="name"></v-text-field>
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
  name: 'HomeView',
  data: function() {
    return {
      ime: "Loris",
      prezime: "Lukić",
      commits: [],
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
  async mounted() {
    let rezultat0 = await fetch("https://api.agify.io?name=michael");
    let rezultat1 = await fetch("https://api.genderize.io?name=peter");
    let rezultat2 = await fetch("https://api.nationalize.io?name=michael");
    
    let podaci = await rezultat0.json();
    console.log(rezultat0);
    console.log(rezultat1);
    console.log(rezultat2);
  },
};
</script>
