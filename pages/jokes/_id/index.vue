<template>
  <div>
    <nuxt-link to="/jokes">Back to Jokes</nuxt-link>
    <h2>
      <Joke :joke="joke.joke" />
    </h2>
    <small>Joke ID: {{$route.params.id}}</small>
  </div>
</template>

<script>
import Joke from "../../../components/Joke";
import axios from "axios";
export default {
    components:{
        Joke
    },
    data(){
        return{
            joke:{}
        }
    },
    async created(){
        const config = {
            headers:{
                'Accept':'application/json'
            }
        }

        try {
            const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`,config);
            this.joke = res.data;
        } catch (err) {
            console.log(err)
        }
    },
    head(){
      return{
          title:this.joke.joke,
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