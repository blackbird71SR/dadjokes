<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <h1>Jokes</h1>
    <Joke v-for="joke in jokes" v-bind:key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from 'axios';
import Joke from '../../components/Joke';
import SearchJokes from "../../components/SearchJokes"

export default {
  components:{
    Joke,
    SearchJokes
  },
  data(){
    return{
      jokes:[]
    }
  },
  async created(){
    const config = {
      headers:{
        'Accept':'application/json'
      }
    }
    try {
      const res = await axios.get('https://icanhazdadjoke.com/search',config);
      this.jokes = res.data.results;
    } catch (err) {
      console.log(err)
    }
  },
  methods:{
    async searchText(text){
      const config = {
        headers:{
          'Accept':'application/json'
        }
      }
      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`,config);
        this.jokes = res.data.results;
      } catch (err) {
        console.log(err)
      }
    }
  },
  head(){
      return{
          title:'Jokes!',
          meta:[{
              hid: 'description',
              name: 'description',
              content:'Best place for corny dad jokes'
          }]
      }
  }
}
</script>

<style>

</style>