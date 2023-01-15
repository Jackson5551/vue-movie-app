<script>
    export default {
        name:'HomePageSearch',
        data(){
            return {
                searchQuery: String,
            }
        },
        methods:{
            handleSubmit(e){
                e.preventDefault()
            }
        }
    }
</script>

<template>
            <div class="h-fit p-5 m-5 w-[80%] max-sm:w-full max-sm:m-0">
                <form className='' @submit="handleSubmit">
            
                    <div class='flex justify-center items-center max-sm:flex-col'>
                        <div class='max-sm:relative max-sm:w-full max-sm:p-5'>
                            <select
                                class='border-solid border-2 border-[#0d253f] bg-[#0d253f] text-white p-4 w-fit max-sm:w-full rounded-l-2xl max-sm:rounded-2xl'>
                                <option value='' selected>All</option>
                                <option value=''>Movies</option>
                                <option value=''>TV</option>
                                <option value=''>People</option>
                            </select>
                        </div>
                        <div class='relative w-full'>
            
                            <input type="text"
                                class="block p-4 w-full text-sm text-slate-800 bg-white border-solid border-2 border-transparent focus:ring-transparent focus:border-blue-500 max-sm:rounded-2xl"
                                placeholder="Search Movies, TV Shows, People..." required />
                        </div>
                        <div class='max-sm:relative max-sm:w-full max-sm:p-5'>
                            <button type='submit'
                                class='border-solid border-2 border-[#0d253f] bg-[#0d253f] text-white p-4 w-full rounded-r-2xl max-sm:rounded-2xl'>Search</button>
                        </div>
                    </div>
            
                </form>
                <span className='flex justify-center items-center p-2 text-slate-400'>Powered by - <a
                        href='https://www.themoviedb.org/' target='_blank'>TMDb</a></span>
            </div>
</template>