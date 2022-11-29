<script>
export default {
    methods: {
        onSubmit() {
          
            if(!this.movie || !this.genre || !this.year) {
                return;
            }
            this.$emit('movie-added', [this.movie, this.genre, this.year])
           this.movie="";
            this.genre="";
            this.year="";
        }
    }   
}   
</script>

<template>
    <form @submit.prevent="onSubmit">
        <div class="mb-4">
            <label for="movie">Movie: </label>
            <input class="shadow appearance-none border rounded focus:outline-none focus:shadow-outline" type="text" id="movie" v-model.lazy.trim="movie"/><br/>  
        </div> 
        <div class="mb-4">
            <label for="genre">Genre: </label>
             <input class="shadow appearance-none border rounded focus:outline-none focus:shadow-outline" type="text" id="genre" v-model.lazy.trim="genre" /><br/>
        </div>
        <div class="mb-4">
             <label for="year">Year: </label>
            <input class="shadow appearance-none border rounded focus:outline-none focus:shadow-outline" type="text" id="year" v-model.lazy.trim.number="year" /> 
       </div>    
    
      <div class="flex space-x-4 px-2">
      <button class="shadow bg-blue-400 hover:bg-red-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded" type="submit">
        Add
      </button>
   
    
   
   
    </div>
    </form>
</template>