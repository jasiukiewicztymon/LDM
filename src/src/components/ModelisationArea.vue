<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div class="w-[10000px] h-[10000px] p-[20px]">
            <div class="w-[200px] h-[300px] bg-blue-300">

            </div>
        </div>
    </div>
</template>

<script>
import datas from '../data.json'

export default {
    components: {
    },
    data() {
        return {
           data: datas,
        }
    },
    methods: {
        checkname() {
            if (document.getElementById('plus-info').classList.contains('on')) {
                console.log(this.data)
                document.getElementById('main-box').onmousedown = function(e) {
                    console.log([e.clientX, e.clientY])
                }
            }
            else if (document.getElementById('trash-info').classList.contains('on')) {
                console.log('2')
            }
            else if (document.getElementById('pencil-info').classList.contains('on')) {
                console.log('3')
            }
            else if (document.getElementById('slash-lg-info').classList.contains('on')) {
                console.log('4')
            }
        }
    },
    mounted() {
        document.getElementById('main-box').scrollTop = 5000;
        document.getElementById('main-box').scrollLeft = 5000;
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
