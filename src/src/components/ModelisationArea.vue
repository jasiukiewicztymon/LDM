<template>
    <div @click="checkname" id="main-box" class="absolute left-[50%] overflow-auto -translate-x-[50%] top-[16vw] md:top-[12vw] lg:top-[9vw] w-[90vw] h-[82.5vh] lg:h-[75vh]">
        <div @mousedown="mousedown($event)" @mousemove="mousemove($event)" @mouseleave="this.drag.isDown = false" @mouseup="this.drag.isDown = false" :class="{active: this.drag.isDown}" class="w-[10000px] h-[10000px] p-[20px]">
            <div class="absolute top-[5000px] left-[20px] w-[100px] h-[100px] bg-red-100"></div>
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
           drag: {
               isDown: false,
               startX: 0,
               startY: 0,
               scrollLeft: 0,
               scrollTop: 0,
           }
        }
    },
    methods: {
        checkname() {
            if (document.getElementById('plus-info').classList.contains('on')) {
                console.log(this.data)
                document.getElementById('main-box').onmousedown = function(e) {
                    console.log(e.offsetX)
                    console.log(e.offsetY)
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
        },
        replace() {
            document.getElementById('main-box').scrollTop = 5000;
            document.getElementById('main-box').scrollLeft = 5000;
        },
        mousedown(e) {
            let element = document.getElementById('main-box');

            this.drag.isDown = true;
            this.drag.startX = e.pageX - element.offsetLeft;
            this.drag.startY = e.pageY - element.offsetTop;
            this.drag.scrollLeft = element.scrollLeft;
            this.drag.scrollTop = element.scrollTop;
        },
        mousemove(e) {
            let element = document.getElementById('main-box');
            if (this.drag.isDown) {
                e.preventDefault();
                let x = e.pageX - element.offsetLeft;
                let y = e.pageY - element.offsetTop;
                let wx = (x - this.drag.startX) * 3;
                let wy = (y - this.drag.startY) * 3;
                element.scrollLeft = this.drag.scrollLeft - wx;
                element.scrollTop = this.drag.scrollTop - wy;
            }
        }
    },
    created() {
        window.addEventListener('load', this.replace)
    },
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
