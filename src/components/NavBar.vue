<script>
export default {
    name: 'NavBar',
    computed: {
        homePage() {
            if (this.$route.path !== '/') {
                return true
            } else {
                return false
            }
        }
    }
}
</script>

<template>
    <div class="flex justify-around bg-slate-800 text-white h-fit max-sm:flex-col" v-show="homePage">
        <div className='flex justify-center items-center'>
            <RouterLink to="/" class="p-2 text-4xl flex justify-between items-center text-transparent bg-clip-text bg-gradient-to-l from-blue-500 to-cyan-500 rounded-2xl">
                <i class="bi bi-film"></i>
                <span class="p-2">MovieDb</span>
            </RouterLink>
        </div>
    </div>
</template>

<style>

</style>