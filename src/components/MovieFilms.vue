<template>

  <div>
    <form @submit.prevent>
      <div class="inner-mars">
        <input type="text" v-model="targetMovie">
        <button @click="addFavoriteMovie">Добавить фильм</button>
      </div>
    </form>

    <div v-for="movie in favoriteMovies" :key="movie.id">
      {{ movie.name }}
      <button @click="deleteMovie(movie.id)">delete</button>
    </div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      favoriteMovies: [
        {id: 1, name: 'Batman'},
        {id: 2, name: 'Robin'},
        {id: 3, name: 'Joker'},
        {id: 4, name: 'Karl'}
      ],
      targetMovie: ''
    }
  },
  methods: {
    deleteMovie(movieId) {
      this.favoriteMovies = this.favoriteMovies.filter(m => m.id !== movieId);
      console.log(this.favoriteMovies);
    },

    addFavoriteMovie() {
      if (this.targetMovie !== '') {
        const pushMovie = {
          id: crypto.randomUUID(),
          name: this.targetMovie
        }
        this.favoriteMovies.push(pushMovie);
        this.targetMovie = '';
        console.log(this.favoriteMovies);
      }
    }
  }
}
</script>

<style>

.inner-mars {
  margin-top: 20px;
  background-color: #d3d3d3;
}
</style>
