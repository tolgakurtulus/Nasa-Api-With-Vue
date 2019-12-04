<template>
  <div class="search">
    <h2>What Do You Want ? Just You Write</h2>
    <form v-on:submit.prevent="getResult(query)">
      <input class="renk" type="text" placeholder="Search" v-model="query" />
    </form>
    <div class="results" v-if="results">
      <div v-for="result in results" v-bind:key="result">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult(query){
      axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then( response => {
        console.log(response.data.collection.items);
        this.results = response.data.collection.items;
      });
    }  
  }   
} 
</script>

<style scoped>
h1, h2 {
  font-weight: bold;
  color: orange; 
}
.results img{
  height: 300px;
  margin-bottom: 10px;
  margin-top: 50px;
}

.renk{

  color: black;
  font-weight: bold;
  background-color:orange;
}




</style>
