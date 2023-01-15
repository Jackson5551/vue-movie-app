<script>
export default {
    name:'ResultCard',
    props:{
        result:String,
        category:String,
        img_path:String,
    },
    data(){
        return{

        }
    },
    methods:{

    }
}
</script>
<template>
    <li class="m-3 box-border">
        <router-link :to="`/movies/${result.id}`">
            <img :src="`https://image.tmdb.org/t/p/w500${img_path}`" alt=""
            class="w-96 h-full min-h-[550px] max-h-full hover:shadow-2xl border-solid border-transparent border-2 hover:shadow-white/50 hover:border-solid hover:border-white hover:border-2 box-border hover:box-border rounded-2xl">
        </router-link>
    </li>
</template>