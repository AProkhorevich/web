<template>
    <a class="btn btn-primary" data-bs-toggle="collapse" :href="'#collapse-' + episode.episode_id" role="button"
        aria-expanded="false" :aria-controls="'collapse-' + episode.episode_id">
        {{ episode.episode_id }} - {{ episode.title }}
    </a>
    <div class="py-2 collapse" :id="'collapse-' + episode.episode_id">
        <div class="card w-75 mx-auto">
            <div class="card-title px-2 py-auto row">
                <h5 class="text-start text-dark col-6">{{ episode.title }}</h5>
                <div class="col-6 text-end">
                    <button v-if="isFavs" class="btn btn-danger" @click="favsAction(episode)">
                         Delete from favorites
                    </button>

                    <button v-else class="btn btn-success" @click="favsAction(episode)">
                        Add to favorites
                    </button>
                </div>
            </div>
            <div class="card card-body">
                <div class="content row">
                    <div class="col-6">
                        season #{{ episode.season }}<br>
                        Air date: {{ air_date }}
                    </div>
                    <div class="col-6">
                        <h5>Characters:</h5>
                        <p v-for="character in episode.characters" :key="character">
                            {{ character }}
                        </p>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>

export default {
    name: 'v-Episode',
    methods: {

    },
    props: {
        episode: Object,
        favsAction: Object,
        isFavs: Boolean
    },
    mounted: function () {
        console.log(this.episode);
    }
}
</script>

<style scoped>
</style>
