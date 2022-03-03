<template>
    <nav class="h-[14vw] md:h-[10vw] lg:h-[7vw] w-screen absolute">
        <h1 class="hidden lg:flex">Logical data models Generator</h1>
        <div id="tools" class="scale-125 lg:scale-100 right-[50%] translate-x-[50%] lg:translate-x-[0%] absolute lg:right-[2.5vw] top-[50%] -translate-y-[50%] flex">
            <div id="plus-info">
                <img src="../assets/plus.svg" id="svg-plus" class="mr-[3vw] duration-500">
            </div>
            <div id="trash-info">
                <img src="../assets/trash.svg" id="svg-trash" class="mr-[3vw] duration-500">
            </div>
            <div id="pencil-info">
                <img src="../assets/pencil.svg" id="svg-pencil" class="mr-[3vw] duration-500">
            </div>
            <div id="slash-lg-info">
                <img src="../assets/slash-lg.svg" id="svg-slash-lg" class="mr-[3vw] duration-500">
            </div>
            <div id="arrow-bar-up-info">
                <img src="../assets/arrow-bar-up.svg" id="svg-arrow-bar-up" class="mr-[3vw] duration-500">
            </div>
        </div>
    </nav>
</template>

<style lang="sass" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@500&display=swap')

    $nav: #41bf82
    $navtext: #fff
    $fontglobal: 'Open Sans', sans-serif
    * 
        font-family: $fontglobal
        nav
            background: $nav
            color: $navtext
            line-height: 7vw
            h1
                margin-left: 1.5vw
                font-size: 2vw
            #tools
                img
                    width: 3vw
                    filter: invert(100%)
                #plus-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        &::after
                            content: 'Add a table'
                            position: absolute
                            top: 0.5vw
                            left: -0.75vw
                            color: #fff
                            display: flex
                #trash-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        &::after
                            content: 'Delete a table'
                            position: absolute
                            top: 0.5vw
                            left: -1.25vw
                            color: #fff
                            display: flex
                #pencil-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        &::after
                            content: 'Edit a table'
                            position: absolute
                            top: 0.5vw
                            left: -0.75vw
                            color: #fff
                            display: flex
                #slash-lg-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        &::after
                            content: 'Link tables'
                            position: absolute
                            top: 0.5vw
                            left: -0.75vw
                            color: #fff
                            display: flex
                #arrow-bar-up-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        &::after
                            content: 'Export'
                            position: absolute
                            top: 0.5vw
                            left: 0.25vw
                            color: #fff
                            display: flex
</style>