<template>
    <nav class="h-[14vw] md:h-[10vw] lg:h-[7vw] w-screen fixed z-[2]">
        <h1 class="hidden lg:flex">Logical data models Generator</h1>
        <div id="tools" class="scale-125 lg:scale-100 right-[50%] translate-x-[50%] lg:translate-x-[0%] absolute lg:right-[2.5vw] top-[50%] -translate-y-[50%] flex">
            <div :class="{ on: this.newTable }" @click="createTable" id="plus-info" class="before:content-['Add_a_table'] before:left-[-15%] before:hidden lg:hover:before:flex before:absolute before:text-[0.8vw]">
                <img src="../assets/plus.svg" id="svg-plus" class="mr-[4.5vw] lg:mr-[3.5vw] duration-500 scale-[200%] md:scale-[150%] lg:scale-[100%]">
            </div>
            <div :class="{ on: this.delTable }" @click="deleteTable" id="trash-info" class="before:content-['Delete_a_table'] before:left-[-25%] before:hidden lg:hover:before:flex before:absolute before:text-[0.8vw]">
                <img src="../assets/trash.svg" id="svg-trash" class="mr-[4.5vw] lg:mr-[3.5vw] duration-500 scale-[200%] md:scale-[150%] lg:scale-[100%] ">
            </div>
            <div :class="{ on: this.editTable }" @click="editionTable" id="pencil-info" class="before:content-['Edit_a_table'] before:left-[-15%] before:hidden lg:hover:before:flex before:absolute before:text-[0.8vw]">
                <img src="../assets/pencil.svg" id="svg-pencil" class="mr-[4.5vw] lg:mr-[3.5vw] duration-500 scale-[200%] md:scale-[150%] lg:scale-[100%] ">
            </div>
            <div :class="{ on: this.linkTable }" @click="linkingTable" id="slash-lg-info" class="before:content-['Link_tables'] before:left-[-15%] before:hidden lg:hover:before:flex before:absolute before:text-[0.8vw]">
                <img src="../assets/slash-lg.svg" id="svg-slash-lg" class="mr-[4.5vw] lg:mr-[3.5vw] duration-500 scale-[200%] md:scale-[150%] lg:scale-[100%] ">
            </div>
            <div :class="{ on: this.exportTable }" @click="exportingTable" id="arrow-bar-up-info" class="before:content-['Export'] before:left-[-1%] before:hidden lg:hover:before:flex before:absolute before:text-[0.8vw]">
                <img src="../assets/arrow-bar-up.svg" id="svg-arrow-bar-up" class="mr-[4.5vw] lg:mr-[3.5vw] duration-500 scale-[200%] md:scale-[150%] lg:scale-[100%] ">
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    components: {},
    data() {
        return {
            newTable: false, 
            delTable: false,
            editTable: false, 
            linkTable: false,
            exportTable: false,
        }
    },
    methods: {
        createTable() {
            this.newTable = !this.newTable;
            this.delTable = false;
            this.editTable = false;
            this.linkTable = false;
            this.exportTable = false;
        },
        deleteTable() {
            this.newTable = false;
            this.delTable = !this.delTable;
            this.editTable = false;
            this.linkTable = false;
            this.exportTable = false;
        },
        editionTable() {
            this.newTable = false;
            this.delTable = false;
            this.editTable = !this.editTable;
            this.linkTable = false;
            this.exportTable = false;
        },
        linkingTable() {
            this.newTable = false;
            this.delTable = false;
            this.editTable = false;
            this.linkTable = !this.linkTable;
            this.exportTable = false;
        },
        exportingTable() {
            this.newTable = false;
            this.delTable = false;
            this.editTable = false;
            this.linkTable = false;
            this.exportTable = !this.exportTable;
        }
    }
}
</script>

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
                    width: 2.25vw
                    filter: invert(100%)
                #plus-info
                    transition: .5s ease
                    &:hover
                        transform: translateY(-1vw)
                        cursor: pointer
                #trash-info
                    transition: .5s ease
                    &:hover
                        cursor: pointer
                        transform: translateY(-1vw)
                #pencil-info
                    transition: .5s ease
                    &:hover
                        cursor: pointer
                        transform: translateY(-1vw)
                #slash-lg-info
                    transition: .5s ease
                    &:hover
                        cursor: pointer
                        transform: translateY(-1vw)
                #arrow-bar-up-info
                    transition: .5s ease
                    &:hover
                        cursor: pointer
                        transform: translateY(-1vw)
</style>
