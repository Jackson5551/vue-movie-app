<script>
export default {
    name:'MovieView',
    data(){
        return{
            movieId: this.$route.params.id,
            api_key: import.meta.env.VITE_TMDB_API_KEY,
            movieData: Array,
            contentRatings: Array,
            watchProviders: Array,
            recommendations: Array,
            credits:Array,
        }
    },
    methods:{
        async fetchData(url){
            const res = await fetch(url)
            const data = await res.json()
            return data
        }
    },
    async created(){
        this.movieData = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}?api_key=${this.api_key}&language=en-US`)
        this.contentRatings = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/release_dates?api_key=${this.api_key}&language=en-US`)
        this.watchProviders = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/watch/providers?api_key=${this.api_key}&language=en-US`)
        this.recommendations = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/recommendations?api_key=${this.api_key}&language=en-US`)
        this.credits = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/credits?api_key=${this.api_key}&language=en-US`)
    }
}
</script>

<template>
    <div class="bg-gradient-to-r from-cyan-500 to-blue-500">
        <div :style="{ backgroundImage: `url(https://image.tmdb.org/t/p/original${this.movieData.backdrop_path})`}"
        class="w-full h-full bg-center bg-cover bg-no-repeat bg-fixed">
        <div class="backdrop-blur-lg bg-slate-800/50 p-2 h-full min-h-screen">
            <div class="flex h-full w-full min-h-[50vh] max-md:flex-col max-md:items-center">
                <div v-if="this.movieData.poster_path" class="max-md:m-5">
                    <img :src="`https://image.tmdb.org/t/p/w500${movieData.poster_path}`" alt="" class="rounded-2xl min-w-96">
                </div>
            </div>
        </div>
        </div>
    </div>
</template>

<style scoped>

</style>