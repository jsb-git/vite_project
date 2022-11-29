<script>
import MovieCheckboxList from './components/MovieCheckboxList.vue';
import MovieForm from './components/MovieForm.vue';
import uniqueId from 'lodash.uniqueid';


export default {
  name: 'app',
  components: {
    MovieCheckboxList,
    MovieForm
  },
  data() {
    return {
      MovieList: [
        { id: uniqueId('movie-'), label: 'Titanic', genre: 'Romance', year: 1998 },
        { id: uniqueId('movie-'), label: 'SpiderMan', genre: 'Superhero Adventure', year: 2005 },
        { id: uniqueId('movie-'), label: 'The Crow', genre: 'Horror', year: 1989 },
        { id: uniqueId('movie-'), label: 'Harry Potter', genre: 'Fantasy Adventure', year: 1997 }
      ],
      editedId: "",
      result: []


    };
  },
  methods: {
    addMovie(addedMovie) {
      this.MovieList.push({ id: uniqueId('movie-'), label: addedMovie[0], genre: addedMovie[1], year: addedMovie[2] });
    },
    showforedit(movie) {
      var checkboxes = document.getElementsByName("movielist");
      //console.log(checkboxes);
      for (var l = 0; l < checkboxes.length; l++) {
        if (checkboxes[l].checked) {
          //if (this.result.indexOf(checkboxes[l].id) === -1) {
            //this.result.push(checkboxes[l].id)
          //}
          if (!this.result.includes(checkboxes[l].id)) {
            this.result.push(checkboxes[l].id)
          }
        } else {
          //alert(this.result.indexOf(checkboxes[l].id))
          /*if (this.result.indexOf(checkboxes[l].id) === 1 || this.result.indexOf(checkboxes[l].id) === 0) {
            //alert(checkboxes[l].id)
            this.result.splice(this.result.indexOf(checkboxes[l].id), 1)
          }*/
          if (this.result.includes(checkboxes[l].id)) {
            this.result.splice(this.result.indexOf(checkboxes[l].id), 1)
          }
        }
      }
      //console.log(this.result)
      const forms = document.forms[0]
      let arrValues = Object.values(movie); //Convert movie obj to array
      this.editedId = movie.id;
      for (let i = 0; i < forms.length; i++)
        forms.elements[i].value = arrValues[i + 1];

      if (this.result.length === 0) {
        console.log(this.result.length)
        document.forms[0].elements[0].value = "";
        document.forms[0].elements[1].value = "";
        document.forms[0].elements[2].value = "";
        this.editedId = ""
      }
    },
    updatemovie() {
      const movieToEdit = this.MovieList.find((item) => item.id === this.editedId);
      movieToEdit.label = document.forms[0].elements[0].value;
      movieToEdit.genre = document.forms[0].elements[1].value;
      movieToEdit.year = document.forms[0].elements[2].value;
      document.forms[0].elements[0].value = "";
      document.forms[0].elements[1].value = "";
      document.forms[0].elements[2].value = "";
    },
    deletemovie() {
      let n = this.result.length
      for (let i = 0; i < n; i++) {
        const itemIndex = this.MovieList.findIndex((item) => item.id === this.result[i]);
        this.MovieList.splice(itemIndex, 1);
        this.result.splice(this.result.indexOf(this.result[i]),1)
      }
      console.log(this.result.length)
      document.forms[0].elements[0].value = "";
      document.forms[0].elements[1].value = "";
      document.forms[0].elements[2].value = "";
      this.editedId = "";
    }
  }
}
</script>

<template >
  <div id="app">
    <h1>Movie App</h1>
    <ul>
      <MovieCheckboxList v-for="movie in MovieList" :key="movie.id" :label="movie.label" :id="movie.id"
        :genre="movie.genre" :year="movie.year" @checkbox-changed="showforedit(movie)" />
      <div class="flex space-x-4 px-2 py-2">
        <button
          class="shadow bg-blue-400 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
          type="button" @click="updatemovie()">
          Update
        </button>
        <button
          class="shadow bg-blue-400 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
          type="button" @click="deletemovie()">
          Delete
        </button>
      </div>
    </ul><br />
    <movie-form @movie-added="addMovie" id="movieform"></movie-form>






  </div>
</template>



