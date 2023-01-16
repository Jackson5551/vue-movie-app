<script>
import { ref, computed, watch, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import Loading from '../components/Loading.vue';

export default {
    setup() {
        const api_key = import.meta.env.VITE_TMDB_API_KEY;
        const route = useRoute();
        const movieId = route.params.id;
        const loading = ref(true);
        const movieData = ref([]);
        // const movieData = useApi
        const { adult, backdrop_path, belongs_to_collection, budget, genres, homepage, id, imdb_id, original_language, original_title, overview, popularity, poster_path, production_companies, production_countries, release_date, revenue, runtime, spoken_languages, status, tagline, title, video, vote_average, vote_count } = movieData;
        const releaseDateFormatted = ref(null);
        const contentRatings = ref([]);
        const watchProviders = ref([]);
        const recommendations = ref([]);
        const credits = ref([]);
        const fetchData = async (url) => {
            const res = await fetch(url);
            const data = await res.json();
            return data;
        };
        const formatTime = (time) => {
            let hours = Math.floor(time / 60);
            let minutes = time % 60;
            return hours + "h " + minutes + "m";
        };
        onMounted(async () => {
            loading.value = true;
            movieData.value = await fetchData(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${api_key}&language=en-US`);
            contentRatings.value = await fetchData(`https://api.themoviedb.org/3/movie/${movieId}/release_dates?api_key=${api_key}&language=en-US`);
            watchProviders.value = await fetchData(`https://api.themoviedb.org/3/movie/${movieId}/watch/providers?api_key=${api_key}&language=en-US`);
            recommendations.value = await fetchData(`https://api.themoviedb.org/3/movie/${movieId}/recommendations?api_key=${api_key}&language=en-US`);
            credits.value = await fetchData(`https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=${api_key}&language=en-US`);
            releaseDateFormatted.value = new Date(release_date);
            loading.value = false;
        });
        return {
            movieData: movieData,
            contentRatings: contentRatings,
            watchProviders: watchProviders,
            releaseDateFormatted: new Date(release_date),
            formatTime: formatTime,
            loading:loading
        };
    },
    components: { Loading }
}
// export default {
//     name: 'MovieView',
//     data() {
//         return {
//             movieId: this.$route.params.id,
//             api_key: import.meta.env.VITE_TMDB_API_KEY,
//             movieData: Array,
//             contentRatings: Array,
//             watchProviders: Array,
//             recommendations: Array,
//             credits: Array,
//             releaseDateFormatted: Date,
//             contentRating: String,
//         }
//     },
//     methods: {
//         async fetchData(url) {
//             const res = await fetch(url)
//             const data = await res.json()
//             return data
//         },
//         formatTime(time) {
//             let hours = Math.floor(time / 60);
//             let minutes = time % 60;
//             return hours + "h " + minutes + "m"
//         },
//     },
//     computed: {
//     },
//     async created() {
//         this.movieData = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}?api_key=${this.api_key}&language=en-US`)
//         this.contentRatings = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/release_dates?api_key=${this.api_key}&language=en-US`)
//         this.watchProviders = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/watch/providers?api_key=${this.api_key}&language=en-US`)
//         this.recommendations = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/recommendations?api_key=${this.api_key}&language=en-US`)
//         this.credits = await this.fetchData(`https://api.themoviedb.org/3/movie/${this.movieId}/credits?api_key=${this.api_key}&language=en-US`)
//         this.releaseDateFormatted = new Date(this.movieData.release_date)

//         this.watchProviders.length ? this.watchProviders = this.watchProviders.results.US : this.watchProviders
//         console.log(this.watchProviders)
//         // console.log(this.getContentRating('US'))
//     }
// }
</script>

<template>
    <div v-if="loading">
        <Loading/>
    </div>
    <div v-else-if="!loading" class="bg-gradient-to-r from-cyan-500 to-blue-500">
        <div :style="{ backgroundImage: `url(https://image.tmdb.org/t/p/original${movieData.backdrop_path && movieData.backdrop_path})` }"
            class="w-full h-full bg-center bg-cover bg-no-repeat bg-fixed">
            <div class="backdrop-blur-lg bg-slate-800/50 p-2 h-full min-h-screen">
                <div class="flex h-full w-full min-h-[50vh] max-md:flex-col max-md:items-center">
                    <div v-if="this.movieData.poster_path" class="max-md:m-5">
                        <img :src="`https://image.tmdb.org/t/p/w500${movieData.poster_path}`" alt=""
                            class="rounded-2xl min-w-96">
                    </div>
                    <div :class="`flex-col w-full ${movieData.poster_path && 'ml-2'} max-sm:ml-0`">
                        <div class="text-slate-400 bg-slate-800 p-5 h-fit mb-2 rounded-2xl">
                            <span>
                                <a :href="movieData.homepage" target="_blank">
                                    <h1 class="text-4xl text-white hover:text-blue-600">{{ movieData.title }} ({{
                                        movieData.release_date ? releaseDateFormatted.getFullYear() : 'N/A'
                                    }})</h1>
                                </a>
                                <p class="italic">{{ movieData.tagline }}</p>
                            </span>
                            <div class="flex items-center text-slate-500">
                                <p class="text-xs border-2 border-yellow-500 p-1 text-yellow-500 w-fit mt-1 mb-1">PG-13
                                </p>
                                <p class='p-1 pl-2'> &bull; </p>
                                <p class=''>{{ formatTime(movieData.runtime) }}</p>
                                <p class='p-1'> &bull; </p>
                                <p>
                                    <span v-for="genre, index in movieData.genres" class="hover:text-blue-600">
                                        {{ index? ',': '' }}
                                        {{ genre.name }}
                                    </span>
                                </p>
                            </div>
                            <p>{{ movieData.overview }}</p>
                            <div class="text-xs mt-5">
                                <span class="text-white">Producers:</span>
                                <span v-for="company, index in movieData.production_companies" class="">
                                    {{
                                        index? ',': ''
                                    }}
                                    {{
                                        company.name
                                    }}
                                </span>
                            </div>
                        </div>
                        <div class="flex justify-between">
                            <div class="h-fit p-5 text-white flex-col">
                                <div class="flex h-fit p-1 flex-wrap">
                                    <img v-for="provider in watchProviders.buy"
                                        :src="`https://image.tmdb.org/t/p/original${provider.logo_path}`" alt=""
                                        class="rounded-2xl w-12 m-1">
                                </div>
                            </div>
                            <div class="h-fit p-5 text-white flex-col">
                                <div class="flex h-fit p-1 flex-wrap">
                                    <img v-for="provider in watchProviders.flatrate"
                                        :src="`https://image.tmdb.org/t/p/original${provider.logo_path}`" alt=""
                                        class="rounded-2xl w-12 m-1">
                                </div>
                            </div>
                            <div class="h-fit p-5 text-white flex-col">
                                <div class="flex h-fit p-1 flex-wrap">
                                    <img v-for="provider in watchProviders.rent"
                                        :src="`https://image.tmdb.org/t/p/original${provider.logo_path}`" alt=""
                                        class="rounded-2xl w-12 m-1">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>

</style>