<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';
import axios from 'axios';

export default {
  data() {
    return {
        searchText: '',
        movies: []
    };
  },
  components: {
    AppHeader,
    AppMain,
    AppFooter
  },
  methods: {
    search() {
    axios
      .get('https://api.themoviedb.org/3/search/movie', {
      params: {
        api_key: '3a4db1cb907349cc970d7a7e93db75c6&query',
        query: this.searchText
      }
      })
      .then((response) => {
          console.log(response.data.results);
          this.movies = response.data.results;
      });

    }
  },
  /*mounted() {
    axios
      .get(this.baseUrl)
      .then((response) => {
        console.log(response)
        this.characters = response.data.data;
        console.log(this.characters);
    });
  }*/
}

</script>


<template>

  <header>
    <input v-model="searchText" type="text" placeholder="Inserisci nome film">
    <button @click="search()">
      Cerca
    </button>
  </header>

  <main>
    <div>
      <ul>
        <li v-for="(movie, i) in movies" :key="i">
            {{ movies }}
        </li>
      </ul>
    </div>
  </main>
</template>
<style lang="scss">
@use "assets/scss/main" as *;
</style>
