<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <fieldset>
        <legend>Lägg till en film</legend>

        <label for="title-field">Titel:</label>
        <input type="text" id="title-field" v-model="title" class="form-control">

        <label for="rating-field">Betyg:</label>
        <select id="rating-field" v-model="rating" class="form-control">
          <option disabled value="">Välj betyg här...</option>
          <option v-for="num in 5" :value="num" :key="num">{{ num }}</option>
        </select>

        <button type="submit" class="btn btn-success mt-3">Spara film</button>
      </fieldset>
    </form>

    <div class="sorting-buttons">
        <button class="btn btn-light mt-3" @click="sortByTitle">Sortera alfabetiskt</button>
        <button class="btn btn-light mt-3" @click="sortByRate">Sortera efter betyg</button>
    </div>
    
    <legend>Filmer:</legend>

    <ul id="movies">
      <li v-for="(movie, index) in movieList" :key="index">
        <h4>{{ movie.title }}</h4>
        <div class="stars">
          <img v-for="star in movie.stars" :key="star" src="@/assets/star.png" alt="movie star icon">
          <span class="delete-movie-icon" @click="deleteMovie(index)"><img src="@/assets/delete.png" alt="delete movie icon"></span>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.sorting-buttons  {
  float: right;
  display: flex;
  gap: 1rem;
}
.delete-movie-icon:hover {
  cursor: pointer;
}

#movies {
    margin: 0;
    padding: 0;
    height: 40vh;
    overflow: scroll;
}

#movies > li {
    list-style: none;
    background: white;
    margin: 5px;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 5px -12px #999;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#movies > li > div > img {
    margin-right: 10px;
    height: 25px;
}

.delete-movie-icon > img {
    margin-left: 10px;
    border-left: 1px solid gray;
    height: 45px;
    padding: 0 0 0 1rem;
}

.delete-movie-icon {
    cursor: pointer;
}
</style>
<script setup>
import { ref, computed } from 'vue';

const title = ref('');
const rating = ref('');
const movieList = ref([]);

function submitForm() {
  if (!validateInputs(title.value, rating.value)) return;

  const newMovie = {
    title: title.value,
    stars: getStars(parseInt(rating.value))
  };

  movieList.value.push(newMovie);
  title.value = '';
  rating.value = '';
}

function validateInputs(title, rating) {
  if (!title) {
    alert("Måste ange en titel för filmen");
    return false;
  }
  if (rating === '' || rating === 0) {
    alert("Måste ange en betyg för filmen");
    return false;
  }
  return true;
}

function getStars(rating) {
  return Array.from({ length: rating }, () => './assets/images/star.png');
}

function deleteMovie(index) {
  movieList.value.splice(index, 1);
}

function sortByTitle() {
  movieList.value.sort((a, b) => a.title.localeCompare(b.title));
}

function sortByRate() {
  movieList.value.sort((a, b) => b.stars.length - a.stars.length);
}

const sortedMovies = computed(() => movieList.value.slice());
</script>
