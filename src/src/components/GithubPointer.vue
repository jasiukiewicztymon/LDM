<template>
    <a href="https://github.com/jasiukiewicztymon/LDM" target="_blank" rel="noopener noreferrer">
        <div id="tailwind" class="w-screen hidden lg:flex">
            <div id="box" class="bg-[#262626]">
                <p>Check it out on GitHub</p>
                <img src="../assets/github.png">
            </div>
        </div>
    </a>
</template>

<style lang="sass" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@500&display=swap')

    $boxbg: #262626
    $text: #fff
    $fontglobal: 'Open Sans', sans-serif
    * 
        font-family: $fontglobal
        color: $text
        #box
            position: fixed
            right: 2vw
            bottom: 2vw
            height: 3vw
            width: 10vw
            cursor: pointer
            border-radius: 1vw
            padding: 0.25vw
            img
                width: 2.5vw
                height: auto
                filter: invert(100%) 
            p 
                font-size: 0.9vw
                width: 60%
                right: 0.35vw
                position: absolute
</style>