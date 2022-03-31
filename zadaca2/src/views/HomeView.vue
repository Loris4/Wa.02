<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">

  </div>
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
