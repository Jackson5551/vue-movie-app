<script>
import HomePageSearch from '../components/HomePageSearch.vue';
export default {
  name:'HomeView',
  components:{
    HomePageSearch,
  }
}
</script>

<template>
  <div class="bg-gradient-to-r from-cyan-500 to-blue-500 h-screen w-screen flex justify-center items-center">
    <div class="w-full h-full flex flex-col justify-around bg-blur bg-slate-800/60 p-5">
      <div class="flex justify-center">
        <div class="flex justify-center items-center">
          <RouterLink to="/"
            class="text-6xl flex justify-center items-center text-center text-transparent bg-clip-text bg-gradient-to-r from-cyan-500 to-blue-500">
            <i class="bi bi-film"></i>
            <span className='p-2'>MovieDb</span>
          </RouterLink>
        </div>
      </div>
      <div class="rounded-3xl w-full flex justify-center">
        <HomePageSearch/>
      </div>
        <div class='flex flex-col text-slate-400 text-center'>
          <span class='text-white'>Browse today's top...</span>
          <span class='text-2xl'>
            <RouterLink to='/movies'>Movies</RouterLink> &bull;
            <RouterLink to=''>TV</RouterLink> &bull;
            <RouterLink to=''>People</RouterLink>
          </span>
        </div>
    </div>
  </div>
</template>
