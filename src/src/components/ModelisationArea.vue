<template>
    <div id="main-box" class="absolute left-[50%] -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
    </div>
</template>

<script>
export default {
    components: {
    },
    data() {
        return {
           id: 0,
        }
    },
    methods: {
        
    }
}
</script>


<style lang="sass" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@500&display=swap')

    $boxbg: #262626
    $text: #fff
    $fontglobal: 'Open Sans', sans-serif
    * 
        font-family: $fontglobal
        #main-box
            border: 0.25vw solid #000
            border-radius: 1vw
</style>