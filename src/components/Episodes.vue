<template>
  <div class="Episodes">
    <h1>Breaking Bad api</h1>

    <br>

    <h2>Favourite episodes</h2>
    <div watch="favs">
      <div v-for="episode in favs" :key="episode">
        <Episode :episode="episode" :favsAction="deleteFromFavs" :isFavs="true" />
      </div>
    </div>
    <br>

    <h2>All episodes</h2>
    <p v-for="episode in allEpisodes" :key="episode">
      <Episode :episode="episode" :favsAction="addToFavs" :isFavs="false" />
    </p>
  </div>
</template>

<script>
import Episode from './Episode.vue'

export default {
  name: 'v-Episodes',
  data() {
    return {
      favs: []
    }
  },
  components: {
    Episode
  },
  props: {
    allEpisodes: Array,
  },
  methods: {
    addToFavs(ep) {
      var favsTemp = JSON.parse(localStorage.getItem('favs')) ?? [];
      var copy = favsTemp.filter(el => el.episode_id == ep.episode_id);
      if (copy.length > 0) {
        return
      }

      ep.episode_id = ep.episode_id + '_favs';
      favsTemp.push(ep)
      localStorage.setItem('favs', JSON.stringify(favsTemp));
      this.favs = favsTemp;
    },
    deleteFromFavs(ep) {
      var favsTemp = JSON.parse(localStorage.getItem('favs')) ?? [];
      this.favs = favsTemp.filter(e => {
        return e.episode_id != ep.episode_id
      })
      localStorage.setItem('favs', JSON.stringify(this.favs));

    }
  },
  beforeMount: function () {
    if (!JSON.parse(localStorage.getItem('favs'))) {
      alert('favs is empty');
    }
  },
  mounted: function () {
    this.favs = JSON.parse(localStorage.getItem('favs'))
  }
}
</script>

<style scoped>
</style>
