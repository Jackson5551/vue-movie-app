<script>
import ResultCard from '../components/ResultCard.vue'

export default {
    name: 'TopMoviesView',
    data() {
        return {
            api_key: import.meta.env.VITE_TMDB_API_KEY,
            topMovieData: [],
        }
    },
    methods: {
        async getTopMovies() {
            const res = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${this.api_key}&language=en-US`)
            const data = await res.json()
            return data.results
        }
    },
    async created() {
        this.topMovieData = await this.getTopMovies()
    },
    components: {
    ResultCard
},
}
</script>
<template>
    <div class="w-full h-full bg-gradient-to-r from-cyan-500 to-blue-500">
        <div class="min-w-full min-h-full bg-slate-800/90">
            <div class='flex justify-center'>
                <h1 class='text-white text-2xl p-2'>Today's Top Movies</h1>
            </div>
            <ul class="flex flex-wrap justify-center box-border">
                <ResultCard  v-for="result in topMovieData" :result="result" category="movies" :img_path="result.poster_path"/>
            </ul>
        </div>
    </div>
</template>