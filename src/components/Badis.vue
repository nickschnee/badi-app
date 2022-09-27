<template>

  <!-- Filter mit Computed (best practice) -->
  <!-- Filter mit Computed (best practice) -->
  <!-- Filter mit Computed (best practice) -->
  <!-- Filter mit Computed (best practice) -->

  <h1 class=""> Badis mit Computed</h1>

  <h1>Alle {{ computedBadis.length }} Zürcher Badis</h1>

  <button @click="setTempFilter"> Nur warme Badis anzeigen </button> {{tempFilter}}

  <div v-for="meineBadi in computedBadis">

    <div style="color:green;">

      <p> {{meineBadi.name}} </p>

      <p> {{meineBadi.temperature}} </p>

      <p class=""> {{meineBadi.openText}} </p>

    </div>

  </div>

<!-- Filter mit If --> 
<!-- Filter mit If --> 
<!-- Filter mit If --> 
<!-- Filter mit If --> 
<!-- Filter mit If --> 
<!-- Filter mit If --> 

  <h1>Filter mit If-Bedingung (weniger schön) </h1> 
  <h1> Alle {{ meineBadis.length }} Zürcher Badis</h1>

  <button @click="fetchBadis"> Lade Badidaten</button>

  <button @click="setTempFilter"> Nur warme Badis anzeigen </button>

  <div v-if="fetchComplete" v-for="meineBadi in meineBadis">

    <div style="color:red;" v-if="meineBadi.temperature > 19 && tempFilter">

      <p> {{meineBadi.name}} </p>

      <p> {{meineBadi.temperature}} </p>

      <p> {{meineBadi.openText}} </p>

    </div>

  </div>


  <div v-if="fetchComplete" v-for="meineBadi in meineBadis">

    <div style="color:blue;" v-if="!tempFilter">

      <p> {{meineBadi.name}} </p>

      <p> {{meineBadi.temperature}} </p>

      <p> {{meineBadi.openText}} </p>

    </div>

  </div>

</template>

<script>
export default {
  name: 'Badis',
  props: {

  },
  data() {
    return {
      meineBadis: [],
      fetchComplete: false,
      tempFilter: false
    }
  },
  methods: {

    fetchBadis() {

      //Die Grundlage für einen Fetch. Fetch ist eine Funktion, die einen Request an einen Server sendet und das Ergebnis zurückgibt
      //In der ersten Zeile wird der Link zur API definiert. Dieser kann immer angepasst werden.
      let url = 'https://baditicker.herokuapp.com/';
      //Hier startet der Fetch mit der definierten URL.
      fetch(url)
        //Wenn der Fetch erfolgreich war, wird die Antwort in ein Objekt gespeichert.
        .then(response => response.json())
        //Wenn das Objekt gespeichert wurde, wird es in eine Variable gespeichert. Diese Variable heisst "data".
        .then(data => {
          //Hier kann man mit der Variable arbeiten. Entweder das DOM mit Informationen erweitern, oder eine neue Funktion aufrufen.
          //Mit "Console.log(data);" sieht man den Inhalt des Objekts.

          this.meineBadis = data.pools;

          this.fetchComplete = true;

          console.log(this.meineBadis);

          //Ab hier kann man entweder mit der Variable data arbeiten, oder eine funktion aufrufen mit data als Parameter.

          //Beispiel eines Funktionsaufrufs
          //"showSomething(data);"

        })
        //Bei einem Fehler wird dieser gefangen "catch" und eine Fehlermeldung in der Konsole ausgegeben.
        .catch(error => console.log(error))

    },

    setTempFilter() {

      this.tempFilter = !this.tempFilter;

    }



  },
  mounted() {

    this.fetchBadis();

  },

  computed: {

    computedBadis() {

      if (this.tempFilter) {

        var filteredArray = this.meineBadis.filter(function (itm) {
          // console.log(itm.temperature);
          return itm.temperature > 19;
        });

        return filteredArray;

      } else {

        return this.meineBadis;

      }

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
