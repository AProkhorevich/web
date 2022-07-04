<template>
  <Episodes :allEpisodes="this.episodes"/>
</template>

<script>
import Episodes from './components/Episodes.vue'

export default {
  name: 'App',
  data() {
    return {
      episodes: []
    }
  },
  components: {
    Episodes
  },
  methods: {
    async getData() {
      fetch("https://www.breakingbadapi.com/api/episodes")
        .then(async response => {
          const data = await response.json();
          // check for error response
          if (!response.ok) {
            // get error message from body or default to response statusText
            const error = (data && data.message) || response.statusText;
            return Promise.reject(error);
          }
          this.episodes = data;
          console.log(data);
        })
        .catch(error => {
          this.errorMessage = error;
          console.error("There was an error!", error);
        });
    }
  },
  mounted: function() {
    this.getData();
  },
  
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
