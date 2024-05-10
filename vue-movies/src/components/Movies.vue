<script setup>
  /*
  defineProps({
    msg: {
      type: String,
      required: true
    }
  })
  */

  import jquery from 'jquery';
  window.$ = window.jQuery = jquery;

  var movies = $("#movies");

  $("#add-movie-form").on("submit", function(e) {
      // Hindra formuläret från att skicka iväg användaren.
      e.preventDefault();

      // Validera formen
      let title = $("#title-field").val();
      let rating = parseInt($("#rating-field").val());

      // Check för value
      const isValide = validateInputs(title, rating);

      // Add to the list
      if(isValide) {
          const movieList = `
          <li>
              <h4>${title}</h4>
              <div class="stars">
                  ${getStars(rating)}
                  <span class="delete-movie-icon" onClick="deleteMovie(event)"><img src="./images/delete.png" alt="delete movie icon"></span>
              </div>
          </li>
          `;
          movies.append(movieList)
      }  
  });

  /**
   * Validate the input data
   */
  function validateInputs(title, rating) {
      let isValide = true;
      if(title.length < 1) {
          isValide = false;
          alert("Måste ange en titel för filmen");
      }
      
      if(rating == 0) {
          isValide = false;
          alert("Måste ange en betyg för filmen");
      }

      return isValide;
  }

  /**
   * Produce html tags with movie list and stars
   */
  function getStars(rating) {
      let stars = '';
      for(let i = 0; i < rating; ++i) {
          stars = stars + `<img src="./images/star.png" alt="movie star icon">`;
      }
      return stars;
  }

  /**
   * Delete move from list
   */
  function deleteMovie(event) {
      var el = event.target;
      // Get <li> elemtn which is one of the parent element
      const list = el.parentNode.parentNode.parentNode;
      list.remove();
  }
</script>

<template>
  <div class="container">

  <h1>Min filmlista</h1>
  <form id="add-movie-form">
      <fieldset>
          <legend>Lägg till en film</legend>

          <label for="title-field">Titel:</label>
          <input type="text" id="title-field" class="form-control">

          <label for="rating-field">Betyg:</label>

          <select type="text" id="rating-field" class="form-control">
              <option value="0">Välj betyg här...</option>
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
              <option value="5">5</option>
          </select>

          <input type="submit" class="btn btn-success mt-3" value="Spara film">

      </fieldset>
  </form>

  <hr>

  <h2>Filmer</h2>

  <ul id="movies">
          
  </ul>

  </div>
</template>

<style scoped>
  #movies {
      margin: 0;
      padding: 0;
  }

  #movies > li {
      list-style: none;
      background-color: #eee;
      margin: 5px;
      padding: 20px;
      box-shadow: 0 0 5px #999;
  }

  #movies > li > img {
      float: right;
      height: 25px;
      margin-left: 5px;
  }

  .delete-movie-icon {
      cursor: pointer;
  }
</style>